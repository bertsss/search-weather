<template>
	<div class="home">
		<h1>Current Location</h1>
		<BigCard class="big-card-container"/>
        <h2>Other Location</h2>
        <SmallCard class="small-card-container"/>
        <SmallCard class="small-card-container"/>
        <SmallCard class="small-card-container"/>
        <SmallCard class="small-card-container"/>
        <SmallCard class="small-card-container"/>
        <img :src="require('@/assets/plus.png')">
	</div>
</template>

<script>
export default {
	name: 'Home',

	components: {
		BigCard: () => import('../components/BigCard.vue'),
		SmallCard: () => import('../components/SmallCard.vue')
	}
}
</script>

<style lang="scss" scoped>
.home {
	display: flex;
	flex-direction: column;
	padding: 35px 0px;
	text-align: center;

	h1 {
		font-weight: 600;
		font-size: 30px;
		margin-bottom: 45px;
    }

    h2 {
		font-weight: 600;
		font-size: 24px;
		margin-bottom: 30px;
    }

    img {
        cursor: pointer;
        display: block;
        margin: 0px auto;
        width: 50px;
        height: 50px;
    }

    .big-card-container {
        margin-bottom: 50px;
    }

    .small-card-container {
        margin-bottom: 30px;
    }
}
</style>
