<script setup>
	import axios from "axios";
	import { onMounted, ref } from "vue";
	import Plan from "@/components/admin/Plan.vue";

	const env = import.meta.env;
	const plans = ref([]);
	const loading = ref(false);

	async function loadPlans() {
		let config = {
			method: "GET",
			url: `${env.VITE_BE_API}/subscriptions?type=primary`,
		};

		axios
			.request(config)
			.then((res) => {
				console.log(res);
				let data = res.data;
				plans.value = data;
			})
			.catch((error) => {
				console.log(error);
			})
			.finally(() => {});
	}

	onMounted(() => {
		loadPlans();
	});
</script>

<template>
	<div class="content-wrapper pb-0">
		<div class="page-header flex-wrap">
			<h3 class="mb-4">
				Subscription Plans
				<br />
				<span class="h6 text-muted d-inline-block"
					>Select from the plans below and get full access.</span
				>
			</h3>
		</div>

		<div class="row align-items-stretch g-3">
			<div v-for="plan in plans" class="col-md-6">
				<Plan :plan="plan" />
			</div>
			
		</div>
	</div>
</template>
