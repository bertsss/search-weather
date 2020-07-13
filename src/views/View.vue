<template>
	<div class="view">
        <Loading v-if="loading" class="loading"/>

        <div v-else>
            <img :src="require('@/assets/close.png')" @click="$router.push('/')">
            <h1>Manila, Philippines </h1>
            <h4>Forecast for the next 5 days</h4>
            <SmallCard class="small-card-container"/>
            <SmallCard class="small-card-container"/>
            <SmallCard class="small-card-container"/>
            <SmallCard class="small-card-container"/>
            <SmallCard class="small-card-container"/>
        </div>
	</div>
</template>

<script>
export default {
	name: 'View',

	data () {
		return {
			loading: false
		}
	},

	created () {
		this.loading = true
		setTimeout(() => {
			this.loading = false
		}, 1000)
	},

	components: {
		SmallCard: () => import('../components/SmallCard.vue'),
		Loading: () => import('../components/Loading.vue')
	}
}
</script>

<style lang="scss" scoped>
.view {
	display: flex;
	flex-direction: column;
	padding: 35px 0px;
	text-align: center;

	h1 {
		font-weight: 600;
		font-size: 26px;
		margin-bottom: 5px;
    }

    h4 {
        color: #606060;
		font-weight: 400;
		font-size: 18px;
		margin-bottom: 30px;
    }

    img {
        cursor: pointer;
        display: block;
        margin-left: auto;
        width: 20px;
        height: 20px;
    }

    .big-card-container {
        margin-bottom: 50px;
    }

    .small-card-container {
        margin-bottom: 30px;
    }

    .loading {
        margin: 0px auto;
    }
}
</style>
