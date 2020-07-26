<template>
	<div class="page-not-found">
		<!-- <img src="@/assets/img/alert.png"> -->

		<h1>
			Page not found
		</h1>

		<button
			class="_primary"
			@click="$router.push('/')"
		>
			Go Back
		</button>
	</div>
</template>
<script>
export default {
	name: 'PageNotFound'
}
</script>

<style lang="scss" scoped>
	.page-not-found {
		display: flex;
		flex-direction: column;
		align-items: center;
		background-color: #F5F5F5;
		height: 100%;
		padding: 50px 0;

		h1 {
			font-size: 40px;
			margin: 30px 0;
		}

	}
</style>
