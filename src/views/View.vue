<template>
	<div class="view">
        <Loading v-if="loading" class="loading"/>

        <div v-else>
            <img :src="require('@/assets/close.png')" @click="$router.push('/')">
            <h1>Manila, Philippines </h1>
            <h4>Forecast for the next 5 days</h4>
            <SmallCard
                v-for="(item, key) in forecast"
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

	data () {
		return {
			loading: false,
			country: 'PH',
			city: 'Manila',
			forecast: []
		}
	},

	created () {
		this.loading = true
		fetch(`https://community-open-weather-map.p.rapidapi.com/forecast?q=${this.city},${this.country}&units=metric`, {
			method: 'GET',
			headers: {
				'x-rapidapi-host': 'community-open-weather-map.p.rapidapi.com',
				'x-rapidapi-key': '4efb42ea59mshc60e51b3f527ba8p1f76cbjsnd04f08ccbac5'
			}
		}).then(res => res.json()).then(data => {
			this.forecast = data.list.filter(i => i.dt_txt.split(' ')[1] === '09:00:00')
			this.loading = false
		}).catch(err => {
			console.log(err)
			this.loading = false
		})
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
