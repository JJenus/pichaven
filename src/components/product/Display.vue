<template>
	<div class="rainbow bg-primary-app">
		<img
			src="/assets/img/logo.png"
			class="img-auto"
			alt="Logo image"
		/>
	</div>
</template>

<style scoped lang="scss">
	*,
	*::before,
	*::after {
		box-sizing: border-box;
	}

	.rainbow {
		width: 164px;
		height: 164px;
		border-radius: 50%;
		padding: 1.5rem;
		margin: auto;

		display: grid;
		place-content: center;
		text-align: center;

		font-size: 1.5em;

		--border-size: 0.3rem;
		border: var(--border-size) dotted transparent;
		background-image: linear-gradient(
				to right,
				rgb(235 244 246 / var(--opacity)),
				rgb(235 244 246 / var(--opacity))
			),
			conic-gradient(
				from var(--angle),
				rgba(213, 62, 51, 0.5) 0deg 90deg,
				rgba(251, 179, 0, 0.5) 90deg 180deg,
				rgba(55, 122, 245, 0.5) 180deg 270deg,
				rgba(57, 153, 83, 0.5) 270deg 360deg
			);
		background-origin: border-box;
		background-clip: padding-box, border-box;
	}

	/** show a warning in browers that don't support it **/
	.warning {
		margin: 2em;
		padding: 1em;
		border: 1px solid #ccc;
	}
	.warning p {
		margin: 0;
		padding: 0;
		text-align: center;
	}
	/* Animate when Houdini is available */
	@supports (background: paint(houdini)) {
		@property --opacity {
			syntax: "<number>";
			initial-value: 0.5;
			inherits: false;
		}

		@property --angle {
			syntax: "<angle>";
			initial-value: 0deg;
			inherits: false;
		}

		@keyframes opacityChange {
			to {
				--opacity: 1;
			}
		}

		@keyframes rotate {
			to {
				--angle: 360deg;
			}
		}

		.rainbow {
			animation: rotate 4s linear infinite,
				opacityChange 3s infinite alternate;
		}

		/* Hide the warning */
		.warning {
			display: none;
		}
	}

	div {
		display: grid;
		place-content: center;
		gap: 0.5em;

		text-align: center;
		line-height: 1.42;
		font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto",
			"Oxygen", "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans",
			"Helvetica Neue", sans-serif;
	}
</style>
