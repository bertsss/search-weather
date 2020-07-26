<template>
	<div class="view">
        <Loading v-if="loading" class="loading"/>

        <div v-else>
            <img :src="require('@/assets/close.png')" @click="$router.push('/')">
            <h1>{{ item.city }}, {{ item.country }}</h1>
            <h4>Forecast for the next 5 days</h4>
            <SmallCard
                v-for="(item, key) in item.forecast"
                class="small-card-container"
                :key="key"
                :date="new Date(item.dt_txt).toDateString()"
                :weather="item.weather[0].description"
                :temp="Math.round(item.main.temp)"
                :rangeTemp="[Math.floor(item.main.temp_min), Math.ceil(item.main.temp_max)]"
                :icon="item.weather[0].icon"
            />
        </div>
	</div>
</template>

<script>
export default {
	name: 'View',
	props: ['id'],

	data () {
		return {
			item: null,
			loading: false,
			list: JSON.parse(localStorage.getItem('cities'))
		}
	},

	created () {
		this.item = this.list.filter(i => i.city === this.id)[0]
		if (!this.item) this.$router.push('/pagenotfound')
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
