<script setup>
	import { ref } from "vue";

	const features = ref([
		{
			title: "Real-Time Predictions",
			desc: "Our platform offers real-time predictions for all major sports, giving you an edge over other sports bettors.",
		},
		{
			title: "Customizable Notifications",
			desc: "Get notified whenever a prediction changes or a new prediction is available. You can customize your notifications to receive only the information that matters most to you.",
		},
		{
			title: "Detailed Analysis",
			desc: "We provide detailed analysis for every prediction, giving you a deeper understanding of the factors that led to our prediction.",
		},
		{
			title: "Historical Data",
			desc: "Our platform has access to years of historical data for every sport, allowing us to make predictions based on past performance and trends.",
		},
		{
			title: ` User-Friendly Interface`,
			desc: `Our platform is designed to be user-friendly, with a simple and intuitive interface that makes it easy to find the information you need.`,
		},
	]);
</script>
<template>
	<div class="container">
		<div class="row justify-content-center">
			<div class="col-12 col-md-8 text-center mb-2 mb-lg-6">
				<h2 class="display-2 fw-bold">Features</h2>
				<p class="lead">
					And if it’s not listed here, we learn incredibly quickly
				</p>
			</div>
		</div>
		<div class="row justify-content-center">
			<div class="col-12 col-lg-10">
				<div class="card bg-white border-gray-300">
					<div v-for="ft in features" class="border-bottom px-4 py-5">
						<div
							class="row align-items-center justify-content-center"
						>
							<div class="col-md-5 pb-2 pb-md-0">
								<h3 class="h5 mb-3">
									{{ ft.title }}
								</h3>
								<p class="mb-0">
									{{ ft.desc }}
								</p>
							</div>
							<div class="col-md-4 text-md-right">
								<span class="badge bg-success">
									<i class="fa-solid fa-check"></i>
								</span>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>
