<script setup>
	import { RouterView } from "vue-router";
	import { onBeforeMount, onMounted, provide, ref } from "vue";
	import axios from "axios";
	import { user } from "@/stores/user";

	import SideBar from "../components/app/SideBar.vue";
	import NavBar from "../components/app/NavBar.vue";
	import Footer from "../components/product/Footer.vue";


	const env = import.meta.env;
	const sessions = ref([]);
	const appUser = ref(user.getUser());

	provide("user", appUser);

	function loadSessions() {
		let config = {
			method: "GET",
			url: `${env.VITE_BE_API}/users/${user.getUser().id}/sessions`,
		};

		axios
			.request(config)
			.then((response) => {
				const session = user.getSession();
				sessions.value = response.data;

				const check = sessions.value.find(
					(e) => e.deviceId == session.deviceId
				);

				if (!check) {
					user.logout();
				}
			})
			.catch(function (error) {
				console.log(error);
			});
	}

	async function loadUser() {
		// console.log("User id: ", user.getUser().id)
		let config = {
			method: "GET",
			url: `${env.VITE_BE_API}/users/${appUser.value.id}`,
		};

		await axios
			.request(config)
			.then((response) => {
				// console.log("User: ", appUser.value);
				appUser.value = response.data;
			})
			.catch((error) => {
				console.log(error);
			});
	}

	onMounted(() => {
		// loadSessions();
	});

	async function mountChat() {
		const plugin = document.createElement("script");
		plugin.setAttribute(
			"src",
			"//code.tidio.co/vtlaremdhzwtv5fcwxfvtvavtuxg8u6t.js"
		);
		plugin.async = true;
		document.head.appendChild(plugin);
	}

	onBeforeMount(async () => {
		// mountChat();
		await loadUser();
	});
</script>

<template>
	<NavBar />
	<main>
		<!-- PAGE START -->
		<div class="section section-lg pt-5 pt-md-7 bg-gray-200">
			<div class="container">
				<div class="row pt-5 pt-md-0">
					<div class="col-12 col-lg-4 mb-3 mb-lg-0">
						<SideBar />
					</div>
					<div class="col-12 col-lg-8">
						<RouterView />
					</div>
				</div>
			</div>
		</div>
	</main>
</template>

<style scoped>
	/* @import url("../assets/css/imports.css"); */
</style>
