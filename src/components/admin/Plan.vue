<script setup>
	import axios from "axios";
	import { inject, ref } from "vue";
	import { alert } from "../../stores/utility";

	const env = import.meta.env;

	const props = defineProps({
		plan: {
			required: true,
		},
		admin: {
			required: false,
		},
	});

	const user = inject("user");
	const loading = ref(false);

	const form = ref({
		userId: null,
		subscriptionId: null,
		length: 1,
	});

	function join() {
		loading.value = true;
		form.value.userId = user.value.id;
		form.value.subscriptionId = props.plan.id;

		// //console.log(form.value);

		let config = {
			method: "POST",
			data: form.value,
			url: `${env.VITE_BE_API}/user-subscriptions`,
		};

		const userMessage = `Hello ${user.value.name}, please confirm your request.`;
		const planMessage = `SUBSCRIPTION \n\nPlan: ${props.plan.title} \nAmount: $${props.plan.amount}`;
		//console.log(userMessage, planMessage);
		// return;
		axios
			.request(config)
			.then((res) => {
				//console.log(res);
				alert.success("Success", "Chat support to activate");
				setTimeout(() => {
					window.tidioChatApi.open();
					// //console.log(message);
					window.tidioChatApi.messageFromOperator(userMessage);
					window.tidioChatApi.messageFromOperator(planMessage);
				}, 3000);
			})
			.catch((error) => {
				//console.log(error);
			})
			.finally(() => {
				loading.value = false;
			});
	}

	function delet() {
		let config = {
			method: "DELETE",
			url: `${env.VITE_BE_API}/subscriptions/${props.plan.id}`,
		};

		axios
			.request(config)
			.then((res) => {
				//console.log(res);
				window.location.reload();
			})
			.catch((error) => {
				//console.log(error);
			})
			.finally(() => {});
	}
</script>

<template>
	<div class="card shadow position-relative p-4 h-100">
		<div
			v-if="admin"
			style="font-size: 0.8rem"
			class="badge bg-primary text-wihite px-2 rounded-3 position-absolute left-0 top-0 m-2"
		>
			{{ plan.type }}
		</div>
		<a
			v-if="admin"
			class="btn btn-icon btn-outline-danger p-1 px-2 border-0 rounded-1 text-dianger position-absolute end-0 top-0 m-2"
			@click="delet()"
		>
			<i class="bi bi-trash3"></i>
		</a>
		<div class="card-header border-bottom bg-white text-center">
			<h3 class="text-primary mb-4">{{ plan.title }}</h3>
			<span class="d-block">
				<span class="display-2 text-primary fw-bold">
					<span class="align-top font-medium">$</span>
					{{ plan.amount }}
				</span>
				<span class="text-gray font-small">/ {{ plan.duration }}</span>
			</span>
		</div>
		<div class="card-body">
			<p>
				{{ plan.description }}
			</p>

			<div v-if="!admin" class="d-grid">
				<button
					:class="loading ? 'disabled' : ''"
					@click="join()"
					class="btn btn-outline-primary animate-up-1"
				>
					<span
						v-if="loading"
						class="spinner-border spinner-border-sm"
					></span>
					<span v-else>
						<span class="fas fa-plus me-1"></span>
						Subscribe
					</span>
				</button>
			</div>
		</div>
	</div>
</template>
