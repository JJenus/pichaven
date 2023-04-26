<script setup>
	import { ref, inject } from "vue";
	import * as filestack from "filestack-js";
	import axios from "axios";
	import { alert, util } from "../../stores/utility";

	const env = import.meta.env;

	const user = inject("user");

	const tempImg = ref(
		"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRkiIFjCOZ-mMeqxd2ryrneiHedE8G9S0AboA&usqp=CAU"
	);
	const changed = ref(false);

	const apikey = env.VITE_FSHARE_KEY;
	const client = filestack.init(apikey);
	const permitDelete = ref(false);

	const loading = ref(false);
	const imgFile = ref(null);
	const savedImg = ref(false);

	// setTimeout(() => {
	// 	user.value.status = "new";
	// }, 3000);

	function saveImage() {
		changed.value = false;
		client
			.upload(imgFile.value)
			.then((res) => {
				console.log("success: ", res);

				user.value.imgUrl = res.url;
				save();
				savedImg.value = true;
			})
			.catch((err) => {
				console.log(err);
				alert.error("Failed", "Please check your connection.");
			});
	}

	function revert() {
		changed.value = false;
		savedImg.value = false;
		user.value.imgUrl = user.getUser().imgUrl;
	}

	function selectImage() {
		const input = document.querySelector("#select-profile-image");
		input.click();
	}

	function newImage(evt) {
		const input = evt.target;

		if (input.files && input.files[0]) {
			imgFile.value = input.files[0];
			// user.value.imgUrl = URL.createObjectURL(input.files[0]);
			tempImg.value = URL.createObjectURL(input.files[0]);
			changed.value = true;
		}
	}

	function submit($evt) {
		if (!$evt.target.checkValidity()) return;
		loading.value = true;
		save();
	}

	function save() {
		let config = {
			method: "PUT",
			url: `${env.VITE_BE_API}/users`,
			data: user.value,
		};
		axios
			.request(config)
			.then((res) => {
				const data = res.data;
				user.value = data;

				alert.success("Success");
			})
			.catch((err) => {
				alert.error("Failed");
				console.log(err);
			})
			.finally(() => {
				loading.value = false;
			});
	}

	function closeAccount() {
		if (permitDelete.value) {
			loading.value = true;
			user.value.status = "deleted";
			let config = {
				method: "PUT",
				url: `${env.VITE_BE_API}/users`,
				data: user.value,
			};
			axios
				.request(config)
				.then((res) => {
					const data = res.data;
					console.log(data);
					const old = user.getToken();
					old.user = data;
					user.login(old);
					user.value = data;

					alert.success("Account closed");

					setTimeout(() => {
						user.logout();
					}, 2000);
				})
				.catch((err) => {
					alert.error("Failed");
					console.log(err);
				})
				.finally(() => {
					loading.value = false;
				});
		} else {
			alert.info("Check yes to permit action");
		}
	}
</script>

<template>
	<div class="row">
		<div class="col-lg-12">
			<div class="card card-body bg-white border-gray-300 mb-4">
				<h2 class="h5 mb-4">General information</h2>
				<form
					@submit.prevent="submit($event)"
					class="needs-validation border-bottom pb-3 pb-lg-4"
					novalidate
				>
					<div class="row">
						<div class="col-md-6 mb-3">
							<div class="mb-3">
								<label for="first_name">Name</label>
								<input
									class="form-control"
									id="first_name"
									type="text"
									placeholder="Enter your first name"
									v-model="user.name"
									name="name"
									required
								/>
							</div>
						</div>
					</div>

					<div class="row">
						<div class="col-md-6 mb-3">
							<div class="mb-3">
								<label for="email">Email</label>
								<input
									class="form-control"
									id="email"
									type="email"
									name="email"
									v-model="user.email"
									required
								/>
							</div>
						</div>
						<div class="col-md-6 mb-3">
							<div class="mb-3">
								<label for="phone">Phone</label>
								<input
									class="form-control"
									id="phone"
									type="text"
									v-model="user.phone"
									required
								/>
							</div>
						</div>
					</div>
					<h2 class="h5 my-4">Location</h2>
					<div class="row">
						<div class="col-sm-9 mb-3">
							<div class="mb-3">
								<label for="address">Address</label>
								<input
									class="form-control"
									id="address"
									type="text"
									placeholder="Enter your home address"
									v-model="user.address"
									required
								/>
							</div>
						</div>
						<div class="col-sm-3 mb-3">
							<div class="mb-3">
								<label for="zip">ZIP</label>
								<input
									class="form-control"
									id="zip"
									type="text"
									v-model="user.zipcode"
									name="zip"
									required
								/>
							</div>
						</div>
					</div>
					<div class="row">
						<div class="col-sm-6 mb-3">
							<div class="mb-3">
								<label for="city">City</label>
								<input
									class="form-control"
									id="city"
									type="text"
									placeholder="City"
									v-model="user.city"
									name="country"
									required
								/>
							</div>
						</div>
						<div class="col-sm-6 mb-3">
							<label for="country2">Country</label>
							<input
								class="form-control"
								id="zip"
								type="text"
								v-model="user.country"
								name="country"
								required
							/>
						</div>
					</div>
					<div class="mt-2">
						<div class="d-flex mb-3">
							<button
								type="reset"
								class="btn d-nonie btn-primary me-3"
							>
								Cancel
							</button>
							<button type="submit" class="btn btn-secondary-app">
								<span v-if="!loading"> Save All </span>
								<span v-else>
									<span
										class="spinner-grow spinner-grow-sm"
										role="status"
										aria-hidden="true"
									></span>
									Please wait...
								</span>
							</button>
						</div>
					</div>
				</form>
			</div>
			<div class="card card-body bg-white border-gray-300 mb-4">
				<h2 class="h5 mb-4">Select profile photo</h2>
				<div class="row align-items-center">
					<div class="col-lg-7">
						<div class="row">
							<div class="col-lg-12 mb-2 mb-lg-0">
								<div
									class="d-flex align-items-center mb-3 justify-content-start"
								>
									<div class="avatar-lg mb-0">
										<img
											@click="selectImage()"
											:src="
												user.imgUrl
													? util.resizeImg(
															user.imgUrl,
															200
													  )
													: tempImg
											"
											class="rounded-circle"
											alt="change avatar"
										/>
									</div>
									<div v-if="changed && !savedImg">
										<button
											@click="saveImage()"
											:class="loading ? 'disabled' : ''"
											class="btn btn-outline-primary btn-sm ms-2 rounded-pill"
										>
											<span v-if="!loading"> Save </span>
											<span v-else>
												<span
													class="spinner-grow spinner-grow-sm"
													role="status"
													aria-hidden="true"
												></span>
												Please wait...
											</span>
										</button>
									</div>
								</div>
							</div>
							<div class="col-12 mb-3 mb-lg-0">
								<div class="h6 mb-0 mos-lg-3">Your avatar</div>
								<small class="text-gray"
									>JPG, GIF or PNG. Max size of 800K</small
								>
							</div>
						</div>
					</div>
					<div class="col-lg-5 col-12">
						<div class="mb-3">
							<label for="formFile" class="form-label"
								>Select image from device</label
							>
							<input
								type="file"
								accept="image/png, image/gif, image/jpeg"
								@change="newImage($event)"
								id="select-profile-image"
								class="d-none"
							/>
							<button
								@click="selectImage()"
								class="btn btn-outline-primary w-100"
							>
								<i class="fa-solid fa-upload me-2"></i>
								upload
							</button>
						</div>
					</div>
				</div>
			</div>

			<div class="card card-body bg-white border-gray-300">
				<h2 class="h5 text-primary pt-1 pt-lg-3 mt-4">Close account</h2>
				<p>
					When you delete your account, your public profile will be
					deactivated immediately. If you change your mind before the
					14 days are up, sign in with your email and password, and
					we’ll send you a link to reactivate your account.
				</p>
				<div class="form-check mb-4">
					<input
						type="checkbox"
						id="delete-account"
						class="form-check-input"
						v-model="permitDelete"
					/>
					<label for="delete-account" class="form-check-label fs-base"
						>Yes, I want to delete my account</label
					>
				</div>
				<button
					:class="!permitDelete || loading ? 'disabled' : ''"
					@click="closeAccount()"
					type="button"
					class="btn btn-danger"
				>
					<span v-if="!loading"> Close </span>
					<span v-else>
						<span
							class="spinner-grow spinner-grow-sm"
							role="status"
							aria-hidden="true"
						></span>
						Processing...
					</span>
				</button>
			</div>
		</div>
	</div>
</template>
