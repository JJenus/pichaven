<script setup>
	const app = import.meta.env.VITE_APP_NAME;
</script>

<template>
	<footer class="footer pt-6 pb-5 bg-dark text-white">
		<div class="container">
			<div class="row justify-content-between">
				<div class="col-md-4">
					<img
						class="navbar-brand-dark mb-4"
						height="35"
						src="/assets/img/brand/light.svg"
						alt="Logo light"
					/>
					<p>
						Evergreenpicks, the sports prediction platform of the
						future. With our cutting-edge technology, you can make
						smarter bets and win big. Get ready for a new era of
						sports betting.
					</p>
					<ul class="social-buttons mb-5 mb-lg-0">
						<li>
							<a
								aria-label="twitter social link"
								class="icon-white me-2"
								><span class="fab fa-twitter"></span
							></a>
						</li>
						<li>
							<a
								class="icon-white me-2"
								aria-label="facebook social link"
								><span class="fab fa-facebook"></span
							></a>
						</li>
						<li>
							<a
								aria-label="github social link"
								class="icon-white me-2"
								><span class="fab fa-github"></span
							></a>
						</li>
					</ul>
				</div>

				<div class="col-12 col-md-4 mb-5 mb-lg-0">
					<span class="h5">Subscribe</span>
					<p class="text-muted font-small mt-2">
						Join our mailing list. Get amazing deals right in your
						mail.
					</p>
					<form action="#">
						<div class="form-row mb-2">
							<div class="col-12">
								<label
									class="h6 fw-normal text-muted"
									for="exampleInputEmail3"
									>Email address</label
								>
								<input
									type="email"
									class="form-control mb-2"
									placeholder="example@company.com"
									name="email"
									aria-label="Subscribe form"
									id="exampleInputEmail3"
									required
								/>
							</div>
							<div class="col-12 d-grid">
								<button
									type="submit"
									class="btn btn-tertiary"
									data-loading-text="Sending"
								>
									<span>Subscribe</span>
								</button>
							</div>
						</div>
					</form>
					<p class="text-muted font-small m-0">
						We’ll never share your details. See our
						<!-- <a class="text-white" href="#">Privacy Policy</a> -->
					</p>
				</div>
			</div>
			<hr class="bg-secondary my-3 my-lg-5" />
			<div class="row">
				<div class="col mb-md-0">
					<a href="/" class="d-flex justify-content-center mb-3"
						><img
							src="/assets/img/themesberg.svg"
							height="30"
							class="me-2"
							alt="Themesberg Logo"
						/>
						<p class="text-white fw-bold footer-logo-text m-0">
							<span class="h5">{{ app }}</span>
						</p>
					</a>
					<div
						class="d-flex text-center justify-content-center align-items-center"
						role="contentinfo"
					>
						<p class="fw-normal font-small mb-0">
							Copyright ©
							<span class="h5">{{ app }}</span> 2013-<span
								class="current-year"
								>2023</span
							>. All rights reserved.
						</p>
					</div>
				</div>
			</div>
		</div>
	</footer>
</template>
