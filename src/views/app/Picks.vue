<script setup>
	import axios from "axios";
	import { inject, onMounted, ref } from "vue";
	import { user } from "@/stores/user";

	const env = import.meta.env;
	const subscriptions = ref([]);

	const appUser = inject("user");
	
	function openChatApp(){
    window.tidioChatApi.open();
	} 

	async function loadSubscriptions() {
		let config = {
			method: "GET",
			url: `${env.VITE_BE_API}/user-subscriptions/${user.getUser().id}`,
		};

		axios
			.request(config)
			.then((res) => {
				// console.log(res);
				let data = res.data;
				subscriptions.value = data;
			})
			.catch((error) => {
				console.log(error);
			})
			.finally(() => {});
	}

	function status(stat) {
		if (!stat) return "pending";
		return stat;
	}

	onMounted(() => {
		loadSubscriptions();
	});
</script>

<template>
	<div class="content-wrapper pb-0">
		<div class="page-header flex-wrap">
			<h3 class="mb-4">
				Hi, {{ appUser.name }} <br />
				<span class="h6 text-muted d-inline-block"
					>Stake wisely on the selections carefully picked just for
					you</span
				>
			</h3>
		</div>
		<div class="mb-4 card">
			<div class="card-body">
				<h5>Picks</h5>
				<p class="text-muted mb-2">Picks from all subscriptions</p>
				<div class="table-responsive">
					<table class="table table-borderless">
						<th>
							<tr>
								<th>Fixture</th>
								<th>Pick</th>
								<th>Date</th>
							</tr>
						</th>
					</table>
				</div>
				<div class="text-center text-muted my-3">
					Contact support on live chat
				</div>
			</div>
		</div>
		<div class="row">
			<div class="col-xl-12 stretch-card grid-margin">
				<div class="card">
					<div class="card-body">
						<div class="row">
							<div class="col-sm-7">
								<h5>Subscriptions</h5>
								<p class="text-muted">My Subscriptions</p>
							</div>
							<div class="col-sm-5 text-md-right">
								<a
									type="button"
									role="button"
									@click="openChatApp()"
									class="btn btn-icon-text mb-3 mb-sm-0 btn-primary font-weight-normal"
								>
									<i
										class="mdi mdi-email btn-icon-prepend"
									></i
									>Contact support
								</a>
							</div>
						</div>
						<div class="row">
							<div v-for="sub in subscriptions" class="col-sm-4">
								<div class="card mb-3 mb-sm-0">
									<div class="card-body py-3 px-4">
										<p class="m-0 survey-head">
											{{ sub.subscription.title }}
										</p>
										<div
											class="d-flex justify-content-between align-items-end flot-bar-wrapper"
										>
											<div>
												<h3 class="m-0 survey-value">
													{{
														sub.subscription.amount
													}}
												</h3>
												<p
													:class="
														status(sub.status) ==
														'pending'
															? 'text-warning'
															: 'text-success'
													"
													class="m-0 mb-2"
												>
													{{ status(sub.status) }}
												</p>
												<p>
													{{ sub.description }}
												</p>
											</div>
										</div>
									</div>
								</div>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>
