<template>
	<div class="home">
        <Loading
			v-if="loading"
			class="loading"
		/>

        <div v-else>
            <h1>Current Location</h1>
            <BigCard
                class="big-card-container"
                :location='`${currentForecast.city}, ${currentForecast.country}`'
                :weather='currentForecast.forecast.weather[0].description'
                :temp="Math.round(currentForecast.forecast.main.temp)"
                :rangeTemp='[Math.floor(currentForecast.forecast.main.temp_min), Math.ceil(currentForecast.forecast.main.temp_max)]'
                :icon='currentForecast.forecast.weather[0].icon'
            />
            <h2>Other Location</h2>

            <h4 v-if="list.length <= 0">Please add one <span @click="$router.push('/add')">here</span></h4>
            <div v-else>
                <SmallCard
                    class="small-card-container"
                    v-for="(item, key) in list"
                    @click="$router.push(`/view/${item.city}`)"
                    :key="key"
                    :location='`${item.city}, ${item.country}`'
                    :weather='item.forecast[0].weather[0].description'
                    :temp='Math.round(item.forecast[0].main.temp)'
                    :rangeTemp='[Math.floor(item.forecast[0].main.temp_min), Math.ceil(item.forecast[0].main.temp_max)]'
                    :icon='item.forecast[0].weather[0].icon'
                    :isClickable="true"
                />
                <img :src="require('@/assets/plus.png')" @click="$router.push('/add')">
            </div>

        </div>
	</div>
</template>

<script>
export default {
	name: 'Home',

	components: {
		BigCard: () => import('../components/BigCard.vue'),
		SmallCard: () => import('../components/SmallCard.vue'),
		Loading: () => import('../components/Loading.vue')
	},

	data () {
		return {
			list: localStorage.getItem('cities') ? JSON.parse(localStorage.getItem('cities')).reverse() : [],
			storedForecast: localStorage.getItem('currentLoc') ? JSON.parse(localStorage.getItem('currentLoc')) : null,
			currentForecast: null,
			loading: false
		}
	},

	async created () {
		this.loading = true
		await fetch('https://freegeoip.app/json/')
			.then(res => res.json())
			.then(async data => {
				const city = data.city.replace(' City', '')
				if (this.storedForecast && city === this.storedForecast.city) this.currentForecast = this.storedForecast
				else await this.getWeather(city, data.country_name)
				this.loading = false
			})
			.catch(err => {
				console.log(err)
			})
	},

	methods: {
		async getWeather (city, country) {
			await fetch(`https://community-open-weather-map.p.rapidapi.com/forecast?q=${city},${country}&units=metric`, {
				method: 'GET',
				headers: {
					'x-rapidapi-host': 'community-open-weather-map.p.rapidapi.com',
					'x-rapidapi-key': '4efb42ea59mshc60e51b3f527ba8p1f76cbjsnd04f08ccbac5'
				}
			}).then(res => res.json()).then(data => {
				if (data.message) return alert(data.message)
				const obj = {
					city: city,
					country: country,
					forecast: data.list[0]
				}
				this.currentForecast = obj
				localStorage.setItem('currentLoc', JSON.stringify(obj))
			}).catch(err => {
				return alert(err)
			})
		}
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

    h4 {
        font-weight: 600;
    }

    span {
        color: #0ba399;
        cursor: pointer;
    }

    img {
        cursor: pointer;
        display: block;
        margin: 0px auto;
        width: 30px;
        height: 30px;
    }

    .big-card-container {
        margin-bottom: 50px;
    }

    .small-card-container {
        margin-bottom: 30px;

        &:hover{
            cursor: pointer;
        }
    }
}
</style>
