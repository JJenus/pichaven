<script setup>
	import { inject, ref } from "vue";

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
					class="navbar-collapse collapse me-auto"
					id="navbar_global"
				>
					<div class="navbar-collapse-header">
						<div class="row">
							<div class="col-6 collapse-brand">
								<a
									href="https://demo.themesberg.com/pixel-pro/v5/index.html"
									><img
										src="/assets/img/brand/dark.svg"
										alt="Themesberg logo"
								/></a>
							</div>
							<div class="col-6 collapse-close">
								<a
									href="#navbar_global"
									class="fas fa-times"
									data-bs-toggle="collapse"
									data-bs-target="#navbar_global"
									aria-controls="navbar_global"
									aria-expanded="false"
									title="close"
									aria-label="Toggle navigation"
								></a>
							</div>
						</div>
					</div>
				</div>
				<div class="d-flex align-items-center d-md-none">
					<div
						class="profile-thumbnail dashboard-avatar mx-lg-auto me-3"
					>
						<img
							width="46"
							src="/assets/img/team/profile-picture-3.jpg"
							class="rounded-circle border-white"
							alt="img"
						/>
					</div>
				</div>
			</div>
		</nav>
	</header>
</template>

<!-- <style scoped>
	@import url("@/assets/css/imports.css");
</style> -->
