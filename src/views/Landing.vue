<script setup>
	import axios from "axios";
	import { onMounted, provide, ref } from "vue";
	import Navbar from "../components/product/Navbar.vue";
	import Footer from "../components/product/Footer.vue";
	import Features from "../components/product/Features.vue";
	import About from "../components/product/About.vue";
	import Display from "../components/product/Display.vue";
	import AuthModal from "../components/AuthModal.vue";

	const env = import.meta.env;

	const testimonials = ref([]);
	const signIn = ref(true);
	provide("authMode", signIn);

	const attributes = ref([
		{
			att: "Accuracy",
			icon: "fa-solid fa-bullseye",
		},
		{
			att: "Data-driven",
			icon: "fas fa-chart-pie",
		},
		{
			att: "User Satisfaction",
			icon: "fa-solid fa-user-check",
		},
		{
			att: "Timeliness",
			icon: "fa-solid fa-stopwatch-20",
		},
	]);

	function loadTestifiers() {
		let config = {
			method: "GET",
			url: `${env.VITE_BE_API}/testimonials`,
		};

		axios
			.request(config)
			.then((res) => {
				console.log(res);
				let data = res.data;
				testimonials.value = data;
			})
			.catch((error) => {
				console.log(error);
			})
			.finally(() => {});
	}

	async function mountChat() {
		const plugin = document.createElement("script");
		plugin.setAttribute(
			"src",
			"//code.tidio.co/oje9p3zweqxnqqcawyqj6y0krt7adfbb.js"
		);
		plugin.async = true;
		document.head.appendChild(plugin);
	}

	onMounted(() => {
		loadTestifiers();
		mountChat();
	});
</script>

<template>
	<AuthModal />
	<Navbar />
	<main>
		<div class="section-header bg-primary-app pb-0">
			<div class="container">
				<div class="row justify-content-center text-center">
					<div class="col-lg-8">
						<Display />
						<div class="mt-4 mb-5">
							<h1 class="display-2 fw-normal my-4">
								This is
								<span class="text-throuigh fw-bolder">{{
									env.VITE_APP_NAME
								}}</span>
								<br />
								<span style="font-size: 2rem" class=""
									>Winning Streak.</span
								>
							</h1>
							<h5 class="fw-normal text-gray">
								<i class="fa-solid fa-quote-left fs-4"></i>
								Make every bet count with
								<span class="text-primary">
									{{ env.VITE_APP_NAME }}
								</span>

								<span class="fw-bold text-dark">
									– the sports prediction community that never
									goes out of style.
								</span>
							</h5>
						</div>
						<ul class="list-inline text-center mb-0">
							<li class="list-inline-item">
								<a
									class="icon icon-md me-3"
									data-toggle="tooltip"
									data-placement="top"
									title="american football"
								>
									<i class="fas fa-football-ball fs-4"></i>
								</a>
							</li>

							<li class="list-inline-item">
								<a
									class="icon icon-md me-3"
									data-toggle="tooltip"
									data-placement="top"
									title="tennis"
								>
									<i
										class="fa-solid fa-table-tennis-paddle-ball"
									></i>
								</a>
							</li>
							<li class="list-inline-item">
								<a
									class="icon icon-md me-3"
									data-toggle="tooltip"
									data-placement="top"
									title="football"
								>
									<i class="fa-solid fa-futbol fs-4"></i>
								</a>
							</li>
							<li class="list-inline-item">
								<a
									class="icon icon-md"
									data-toggle="tooltip"
									data-placement="top"
									title="basketball"
								>
									<i class="fa-solid fa-basketball fs-4"></i>
								</a>
							</li>
						</ul>
						<div class="text-center mt-4">
							<button
								type="button"
								class="btn btn-tertiary rounded-pill px-4"
								data-bs-toggle="modal"
								data-bs-target="#authModal"
								@click="signIn = false"
							>
								Sign up
							</button>
						</div>
					</div>
				</div>
			</div>
		</div>
		<section class="section section-lg bg-primary-app pb-0">
			<div class="container">
				<div
					class="row justify-content-center align-items-center mb-0 mb-md-3"
				>
					<div
						v-for="att in attributes"
						class="col-6 col-md-atuto text-left g-5 mb-md-0 text-center"
					>
						<div class="mb-0 mb-md-3 text-center">
							<i :class="att.icon" class="fs-2"></i>
						</div>
						<h2 class="h4 m-0 p-0">{{ att.att }}</h2>
					</div>
				</div>
			</div>
		</section>
		<div class="section section-lg bg-primary-app">
			<Features></Features>
		</div>
		<div class="section section-sm bg-primary-app">
			<About />
		</div>
		<div class="section section-lg bg-primary-app pb-0">
			<div class="container">
				<div class="row justify-content-center">
					<div class="col-12 col-md-8 text-center mb-4 mb-lg-6">
						<h2 class="display-2 fw-bold">Testimonials</h2>
						<p class="lead">It's always a joy to be one of us</p>
					</div>
				</div>
				<div class="row align-items-center d-none">
					<div class="col-md-6 col-lg-4 text-center">
						<div class="card border-gray-300 mb-4">
							<div class="card-body py-5">
								<img
									src="/assets/img/clients/airbnb.svg"
									class="img-fluid image-sm"
									alt="Airbnb logo"
								/>
								<span class="d-block mt-3"
									><span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span
								></span>
								<p class="card-text py-4 mb-0">
									Some quick example text to build on the card
									title and make up the bulk of the card's
									content.
								</p>
								<a href="#" class="btn btn-primary btn-sm"
									>See story</a
								>
							</div>
						</div>
					</div>
					<div class="col-md-6 col-lg-4 text-center">
						<div class="card border-gray-300 mb-4">
							<div class="card-body py-5">
								<img
									src="/assets/img/clients/paypal.svg"
									class="img-fluid image-sm"
									alt="Paypal logo"
								/>
								<span class="d-block mt-3"
									><span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span
								></span>
								<p class="card-text py-4 mb-0">
									Some quick example text to build on the card
									title and make up the bulk of the card's
									content.
								</p>
								<a href="#" class="btn btn-primary btn-sm"
									>See story</a
								>
							</div>
						</div>
					</div>
					<div class="col-md-6 col-lg-4 text-center">
						<div class="card border-gray-300 mb-4">
							<div class="card-body py-5">
								<img
									src="/assets/img/clients/ebay.svg"
									class="img-fluid image-sm"
									alt="Ebay logo"
								/>
								<span class="d-block mt-3"
									><span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span
								></span>
								<p class="card-text py-4 mb-0">
									Some quick example text to build on the card
									title and make up the bulk of the card's
									content.
								</p>
								<a href="#" class="btn btn-primary btn-sm"
									>See story</a
								>
							</div>
						</div>
					</div>
					<div class="col-md-6 col-lg-4 text-center">
						<div class="card border-gray-300 mb-4">
							<div class="card-body py-5">
								<img
									src="/assets/img/clients/forbes.svg"
									class="img-fluid image-sm"
									alt="Forbes logo"
								/>
								<span class="d-block mt-3"
									><span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span
								></span>
								<p class="card-text py-4 mb-0">
									Some quick example text to build on the card
									title and make up the bulk of the card's
									content.
								</p>
								<a href="#" class="btn btn-primary btn-sm"
									>See story</a
								>
							</div>
						</div>
					</div>
					<div class="col-md-6 col-lg-4 text-center">
						<div class="card border-gray-300 mb-4">
							<div class="card-body py-5">
								<img
									src="/assets/img/clients/corsair.svg"
									class="img-fluid image-sm"
									alt="Corsair Logo"
								/>
								<span class="d-block mt-3"
									><span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span
								></span>
								<p class="card-text py-4 mb-0">
									Some quick example text to build on the card
									title and make up the bulk of the card's
									content.
								</p>
								<a href="#" class="btn btn-primary btn-sm"
									>See story</a
								>
							</div>
						</div>
					</div>
					<div class="col-md-6 col-lg-4 text-center">
						<div class="card border-gray-300 mb-4">
							<div class="card-body py-5">
								<img
									src="/assets/img/clients/docker.svg"
									class="img-fluid image-sm"
									alt="Docker Logo"
								/>
								<span class="d-block mt-3"
									><span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span>
									<span
										class="star fas fa-star text-warning"
									></span
								></span>
								<p class="card-text py-4 mb-0">
									Some quick example text to build on the card
									title and make up the bulk of the card's
									content.
								</p>
								<a href="#" class="btn btn-primary btn-sm"
									>See story</a
								>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
		<div class="section section-lg bg-primary-app">
			<div class="container">
				<div class="row justify-content-center">
					<div class="col-12 col-md-10 text-center mb-4">
						<h2>Want to contact us?</h2>
						<p>Cool! Let’s</p>
					</div>
				</div>
				<div class="row mb-5 mb-lg-6 justify-content-center">
					<div class="col-12 col-sm-4 text-center">
						<div class="icon-box mb-4">
							<div class="icon icon-secondary-app mb-4">
								<span class="fas fa-message"></span>
							</div>
							<h2 class="h5 icon-box-title">Live chat</h2>
							<span>Available</span>
							<div class="text-small text-gray">
								24/7
							</div>
						</div>
					</div>
					<div class="col-12 col-sm-4 text-center">
						<div class="icon-box mb-4">
							<div class="icon icon-secondary-app mb-4">
								<span class="far fa-paper-plane"></span>
							</div>
							<h2 class="h5 icon-box-title">Email</h2>
							<a href="mailto:support@evergreenpicks.com"
								><span
									class="__cf_email__"
									data-cfemail="472f222b2b2807332f222a2234252235206924282a"
									>support@evergreenpicks.com</span
								></a
							>
						</div>
					</div>
				</div>
			</div>
		</div>
	</main>
	<Footer />
</template>
