<script setup>
	import { inject, onMounted, ref } from "vue";
	import axios from "axios";
	import { user } from "../stores/user";
	import { alert } from "../stores/utility";

	const env = import.meta.env;

	const signIn = inject("authMode");
	const loadingReg = ref(false);

	const form = ref({
		name: null,
		email: null,
		password: null,
		cPassword: null,
	});

	const regError = ref(null);
	const loginError = ref(null);

	function register() {
		regError.value = null;

		if (loadingReg.value) {
			return;
		}
		if (
			!form.value.email ||
			!form.value.name ||
			!form.value.password ||
			!form.value.cPassword
		) {
			regError.value = "Please fill form correctly";
			alert.error(regError.value);
			return;
		}

		console.log(regError.value);

		if (form.value.password !== form.value.cPassword) {
			regError.value = "Passwords don't match";
			alert.error(regError.value);
			return;
		}

		loadingReg.value = true;

		const { name, email, password } = form.value;
		console.log(email);

		let config = {
			method: "Post",
			url: `${env.VITE_BE_API}/auth/register`,
			data: {
				name,
				email,
				password,
			},
		};

		axios
			.request(config)
			.then((response) => {
				console.log(response.data);
				if (response.data.error) {
					regError.value = response.data.error;
					alert.error(regError.value);
				} else {
					user.login(response.data);
					alert.success("Signing you in. Please wait.");
					window.location.href = "/app";
				}
			})
			.catch(function (error) {
				console.log(error);
				alert.error("Failed to login");
			})
			.finally(() => {
				loadingReg.value = false;
			});
	}

	function sumitLogin() {
		if (loadingReg.value) {
			return;
		}
		if (!form.value.email || !form.value.password) {
			loginError.value = "Please fill form correctly";
			alert.error(loginError.value);
			return;
		}

		console.log(loginError.value);

		loadingReg.value = true;

		const { email, password } = form.value;
		console.log(email);

		let config = {
			method: "Post",
			url: `${env.VITE_BE_API}/auth/login`,
			data: {
				email,
				password,
			},
		};

		axios
			.request(config)
			.then((response) => {
				console.log(response.data);
				if (response.data.error) {
					loginError.value = response.data.error;
					alert.error(loginError.value);
				} else {
					user.login(response.data);
					alert.success("Authorized");
					window.location.href = "/app";
				}
			})
			.catch(function (error) {
				console.log(error);
			})
			.finally(() => {
				loadingReg.value = false;
			});
	}

	onMounted(() => {});
</script>

<template>
	<div
		class="modal fade"
		id="authModal"
		tabindex="-1"
		role="dialog"
		aria-labelledby="authModal"
		aria-hidden="true"
	>
		<div
			class="modal-dialog modal-dialog-centered modal-fullscreen-sm-down"
			role="document"
		>
			<div class="modal-content rounded">
				<div class="modal-body p-0">
					<div class="card border-gray-300 p-3 px-md-4">
						<button
							type="button"
							class="btn-close ms-auto"
							data-bs-dismiss="modal"
							aria-label="Close"
						></button>
						<div
							v-if="signIn"
							class="card-header border-0 bg-white text-center pb-0"
						>
							<h2 class="h4">Sign in to our platform</h2>
							<span
								>Login here using your username and
								password</span
							>
						</div>
						<div
							v-else
							class="card-header border-0 bg-white text-center pb-0"
						>
							<h2 class="mb-0 h5">Create Account</h2>
						</div>
						<div class="card-body">
							<form
								@submit.prevent="sumitLogin()"
								v-if="signIn"
								class="needs-validation mt-4"
								novalidate
							>
								<p
									v-if="loginError != null"
									class="alert alert-danger p-3 py-1"
								>
									{{ loginError }}
								</p>
								<!-- Form -->
								<div class="form-group mb-4">
									<label for="exampleInputEmailModal"
										>Your Email</label
									>
									<div class="input-group">
										<span
											class="input-group-text"
											id="basic-addon1"
											><span
												class="fas fa-envelope"
											></span
										></span>
										<input
											type="email"
											id="email"
											class="form-control"
											name="email"
											placeholder="Email address here"
											required
											v-model="form.email"
										/>
									</div>
								</div>
								<!-- End of Form -->
								<div class="form-group">
									<!-- Form -->
									<div class="form-group mb-4">
										<label for="s-pass"
											>Your Password</label
										>
										<div class="input-group">
											<span
												class="input-group-text"
												id="password"
												><span
													class="fas fa-unlock-alt"
												></span
											></span>
											<input
												type="password"
												class="form-control"
												name="password"
												id="password"
												placeholder="**************"
												required
												v-model="form.password"
											/>
										</div>
									</div>
									<!-- End of Form -->
									<div
										class="d-flex justify-content-between align-items-center mb-4"
									>
										<div class="form-check">
											<input
												class="form-check-input"
												type="checkbox"
												value=""
												id="defaultCheck55"
											/>
											<label
												class="form-check-label mb-0"
												for="defaultCheck55"
											>
												Remember me
											</label>
										</div>
										<div>
											<a
												href="#"
												class="small d-none text-right"
												>Lost password?</a
											>
										</div>
									</div>
								</div>
								<div class="d-grid">
									<button
										type="submit"
										class="btn btn-primary"
									>
										<span v-if="!loadingReg">
											Sign in
										</span>
										<span v-else>
											<span
												class="spinner-grow spinner-grow-sm"
												role="status"
												aria-hidden="true"
											></span>
											Loading...
										</span>
									</button>
								</div>
								<p class="mt-4 text-center">
									Not registered?
									<a
										role="button"
										@click="signIn = false"
										class="fw-bold text-underline"
										>Create account</a
									>
								</p>
							</form>

							<form
								v-else
								@submit.prevent="register()"
								class="needs-validation"
								novalidate
							>
								<p
									v-if="regError != null"
									class="alert alert-danger p-3 py-1"
								>
									{{ regError }}
								</p>
								<div class="form-group mb-4">
									<label for="exampleInputEmailModal2"
										>Your Name</label
									>
									<div class="input-group">
										<span class="input-group-text" id="name"
											><span class="fas fa-user"></span
										></span>
										<input
											type="text"
											id="name"
											class="form-control"
											name="name"
											placeholder="Enter Name"
											required
											v-model="form.name"
										/>
									</div>
								</div>
								<!-- Form -->
								<div class="form-group mb-4">
									<label for="exampleInputEmailModal2"
										>Your Email</label
									>
									<div class="input-group">
										<span
											class="input-group-text"
											id="basic-addon3"
											><span
												class="fas fa-envelope"
											></span
										></span>
										<input
											type="email"
											id="email"
											class="form-control"
											name="email"
											placeholder="Email address here"
											required
											v-model="form.email"
										/>
									</div>
								</div>
								<!-- End of Form -->
								<div class="form-group">
									<!-- Form -->
									<div class="form-group mb-4">
										<label for="exampleInputPasswordModal3"
											>Your Password</label
										>
										<div class="input-group">
											<span
												class="input-group-text"
												id="password"
												><span
													class="fas fa-unlock-alt"
												></span
											></span>
											<input
												type="password"
												class="form-control"
												name="password"
												placeholder="**************"
												required
												v-model="form.password"
											/>
										</div>
									</div>
									<!-- End of Form -->
									<!-- Form -->
									<div class="form-group mb-4">
										<label for="exampleInputPasswordModal4"
											>Confirm Password</label
										>
										<div class="input-group">
											<span
												class="input-group-text"
												id="cpassword"
												><span
													class="fas fa-unlock-alt"
												></span
											></span>
											<input
												type="password"
												id="cpassword"
												class="form-control"
												name="cpassword"
												placeholder="**************"
												required
												v-model="form.cPassword"
											/>
										</div>
									</div>
									<!-- End of Form -->
									<div class="form-check mb-4">
										<input
											class="form-check-input"
											type="checkbox"
											value=""
											id="defaultCheck66"
										/>
										<label
											class="form-check-label text-dark"
											for="defaultCheck66"
										>
											I agree to the
											<a href="#" class="text-underline"
												>terms and conditions</a
											>
										</label>
									</div>
								</div>
								<div class="d-grid">
									<button
										type="submit"
										class="btn btn-primary"
									>
										Sign in
									</button>
								</div>
								<p class="mt-4 text-center">
									Already have an account?
									<a
										role="button"
										@click="signIn = true"
										class="fw-bold text-underline"
										>Login here</a
									>
								</p>
							</form>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>
