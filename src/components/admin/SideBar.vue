<script setup>
	import { user } from "../../stores/user.js";
</script>

<template>
	<div class="card d-none d-lg-block border-gray-300 p-2">
		<div
			class="card-header bg-white border-0 text-center d-flex flex-row flex-lg-column align-items-center justify-content-center px-1 px-lg-4"
		>
			<div class="profile-thumbnail dashboard-avatar mx-lg-auto me-3">
				<img
					src="../../assets/img/team/profile-picture-3.jpg"
					class="card-img-top rounded-circle border-white"
					alt="Bonnie Green Portrait"
				/>
			</div>
			<span class="h5 my-0 my-lg-3 me-3 me-lg-0">Hi, Bonnie!</span>
			<a href="#" class="btn btn-gray-300 btn-xs"
				><span class="me-2"
					><span class="fas fa-sign-out-alt"></span></span
				>Sign Out</a
			>
		</div>
		<div class="card-body p-2 d-none d-lg-block">
			<div class="list-group dashboard-menu list-group-sm">
				<a
					href="account.html"
					class="d-flex list-group-item border-0 list-group-item-action active"
					>Overview
					<span class="icon icon-xs ms-auto"
						><span class="fas fa-chevron-right"></span
					></span> </a
				><a
					href="settings.html"
					class="d-flex list-group-item border-0 list-group-item-action"
					>Settings<span class="icon icon-xs ms-auto"
						><span class="fas fa-chevron-right"></span
					></span> </a
				><a
					href="my-items.html"
					class="d-flex list-group-item border-0 list-group-item-action"
					>My Items<span class="icon icon-xs ms-auto"
						><span class="fas fa-chevron-right"></span
					></span> </a
				><a
					href="security.html"
					class="d-flex list-group-item border-0 list-group-item-action"
					>Security<span class="icon icon-xs ms-auto"
						><span class="fas fa-chevron-right"></span
					></span> </a
				><a
					href="billing.html"
					class="d-flex list-group-item border-0 list-group-item-action"
					>Billing<span class="icon icon-xs ms-auto"
						><span class="fas fa-chevron-right"></span
					></span> </a
				><a
					href="messages.html"
					class="d-flex list-group-item border-0 list-group-item-action border-0"
					>Messages<span class="icon icon-xs ms-auto"
						><span class="fas fa-chevron-right"></span></span
				></a>
			</div>
		</div>
	</div>

	<div class="card d-lg-none bg-white border-gray-300 mb-4 mb-lg-5">
		<div class="card-body">
			<div class="row align-items-center">
				<div class="col-10 d-flex">
					<a
						href="account.html"
						class="list-group-item list-group-item-action border-0 text-center me-2 active"
						>Overview</a
					>
					<a
						href="settings.html"
						class="list-group-item list-group-item-action border-0 text-center me-2"
						>Settings</a
					>
					<a
						href="my-items.html"
						class="list-group-item list-group-item-action border-0 text-center me-2 d-none d-sm-block border-0"
						>My Items</a
					>
					<a
						href="security.html"
						class="list-group-item list-group-item-action border-0 text-center d-none d-md-block border-0"
						>Security</a
					>
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
									class="fas fa-ellipsis-h icon-secondary fa-lg"
								></span> </span
							><span class="sr-only">Toggle Dropdown</span>
						</button>
						<div class="dropdown-menu">
							<a
								href="my-items.html"
								class="list-group-item list-group-item-action d-sm-none border-0"
								>My Items</a
							>
							<a
								href="security.html"
								class="list-group-item list-group-item-action d-md-none border-0"
								>Security</a
							>
							<a
								href="billing.html"
								class="list-group-item list-group-item-action border-0"
								>Billing</a
							>
							<a
								href="messages.html"
								class="list-group-item list-group-item-action border-0"
								>Messages</a
							>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<style scoped>
	@import url("@/assets/css/imports.css");

	.vh-min {
		min-height: 100vh;
	}
</style>
