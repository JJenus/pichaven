<script setup>
	import { inject, ref } from "vue";
	import { user as auth } from "@/stores/user.js";

	const toggleIcon = ref(false);
	const user = inject("user");

	const env = import.meta.env;

	function toggleMenu() {
		toggleIcon.value = !toggleIcon.value;
		const body = document.querySelector("body");
		if (toggleIcon.value) {
			body.classList.add("sidebar-icon-only");
		} else {
			body.classList.remove("sidebar-icon-only");
		}
	}
</script>

<template>
	<header class="header-global">
		<nav
			id="navbar-main"
			aria-label="Primary navigation"
			class="navbar navbar-main navbar-expand-lg navbar-theme-primary headroom navbar-light"
		>
			<div class="container position-relative">
				<a
					class="navbar-brand me-lg-5 d-flex align-items-center"
					href="/"
				>
					<img
						style="width: 52px; height: 50px"
						class="navbar-brand-dark shadow bg-primary-app p-1 rounded-circle border-white"
						src="/assets/img/logo.png"
						alt="Logo light"
					/>
					<img
						style="width: 52px; height: 50px"
						class="navbar-brand-light rounded-circle shadow p-1 bgf-dark border-white"
						src="/assets/img/logo.png"
						alt="Logo dark"
					/>
				</a>
				
				<div
					class="d-flex flex-wrap align-items-center d-lg-none dropleft"
				>
					<div
						v-if="user.imgUrl"
						class="profile-thumbnail dashboard-avatar mx-lg-auto me-3"
						data-bs-toggle="dropdown"
						aria-haspopup="true"
						aria-expanded="false"
					>
						<img
							width="46"
							:src="user.imgUrl"
							class="rounded-circle border-white"
							alt="img"
						/>
					</div>
					<div
						v-else
						data-bs-toggle="dropdown"
						aria-haspopup="true"
						aria-expanded="false"
						class="p-2 bg-primary-app d-flex align-items-center rounded-circle"
					>
						<i class="fa-solid fa-user-circle fs-1"></i>
					</div>

					<div class="dropdown-menu w-100">
						<a
							class="list-group-item list-group-item-action border-0"
						>
							<a
								@click="auth.logout()"
								role="button"
								class="btn w-100 btn-gray-300 btn-xs"
							>
								<span class="me-2">
									<span
										class="fa-solid fa-sign-out-alt"
									></span>
								</span>
								Sign Out
							</a>
						</a>
					</div>
				</div>
			</div>
		</nav>
	</header>
</template>

<!-- <style scoped>
	@import url("@/assets/css/imports.css");
</style> -->
