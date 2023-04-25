<script setup>
	import { inject, onMounted, ref } from "vue";
	import { user } from "@/stores/user.js";

	const appUser = inject("user");
	const username = ref("unknown");

	const navs = ref([
		{
			name: "Picks",
			path: "picks",
			icon: "",
		},
		{
			name: "Billing",
			path: "billing",
			icon: "",
		},
		{
			name: "Security",
			path: "security",
			icon: "",
		},
		{
			name: "Settings",
			path: "settings",
			icon: "",
		},
	]);

	function disp(i, act = "block") {
		let visib = "";
		if (act == "block") {
			visib = "d-none";
		}
		if (i == 2) {
			visib += " d-sm-" + act;
		} else if (i == 3) {
			visib += " d-md-" + act;
		} else if (i == 4) {
			visib += " d-lg-" + act;
		} else if (act === "none") visib = "d-none";
		else visib = "";

		return visib;
	}

	onMounted(() => {
		if (appUser.name != null) {
			console.log(appUser.name.split(" ")[0]);
			username.value = appUser.name.split(" ")[0];
		}
	});
</script>

<template>
	<div class="card d-none d-lg-block border-gray-300 p-2">
		<div
			class="card-header bg-white border-0 text-center d-flex flex-row flex-lg-column align-items-center justify-content-center px-1 px-lg-4"
		>
			<div class="profile-thumbnail dashboard-avatar mx-lg-auto me-3">
				<img
					src="/assets/img/team/profile-picture-3.jpg"
					class="card-img-top rounded-circle border-white"
					alt="img"
				/>
			</div>
			<span class="h5 my-0 my-lg-3 me-3 me-lg-0"
				>Hi, {{ username }}!</span
			>
			<a href="#" class="btn btn-gray-300 btn-xs">
				<span class="me-2">
					<span class="fa-solid fa-sign-out-alt"></span>
				</span>
				Sign Out
			</a>
		</div>
		<div class="card-body p-2 d-none d-lg-block">
			<div class="list-group dashboard-menu list-group-sm">
				<a
					v-for="nav in navs"
					:href="nav.path"
					class="d-flex list-group-item border-0 list-group-item-action"
				>
					{{ nav.name }}
					<span class="icon icon-xs ms-auto">
						<span class="fa-solid fa-chevron-right"></span>
					</span>
				</a>
			</div>
		</div>
	</div>

	<div class="card d-lg-none bg-white border-gray-300 mb-4 mb-lg-5">
		<div class="card-body">
			<div class="row align-items-center">
				<div class="col-10 d-flex">
					<a
						v-for="(nav, i) in navs"
						:href="nav.path"
						:class="disp(i)"
						class="list-group-item list-group-item-action border-0 text-center me-2 active"
					>
						{{ nav.name }}
					</a>
				</div>
				<div class="col-2 d-flex justify-content-center">
					<div class="btn-group dropleft">
						<button
							class="btn btn-link dropdown-toggle dropdown-toggle-split me-2 m-0 p-0"
							data-bs-toggle="dropdown"
							aria-haspopup="true"
							aria-expanded="false"
						>
							<span class="icon icon-sm"
								><span
									class="fa-solid fa-ellipsis-h icon-secondary fa-lg"
								></span> </span
							><span class="sr-only">Toggle Dropdown</span>
						</button>
						<div class="dropdown-menu">
							<a
								v-for="(nav, i) in navs"
								:href="nav.path"
								:class="disp(i, 'none')"
								class="list-group-item list-group-item-action border-0"
								>{{ nav.name }}</a
							>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<style scoped>
	/* @import url("@/assets/css/imports.css"); */

	.vh-min {
		min-height: 100vh;
	}
</style>
