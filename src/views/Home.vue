<template>
	<div class="home">
		<h1>Current Location</h1>
		<BigCard class="big-card-container"/>
        <h2>Other Location</h2>
        <SmallCard
            class="small-card-container"
            v-for="(item, key) in list"
            @click="$router.push(`/view/${item.id}`)"
            :key="key"
            :location='item.location'
            :temp='item.temperature'
            :weather='item.weather'
            :rangeTemp='item.rangeTemp'
        />
        <img :src="require('@/assets/plus.png')" @click="$router.push('/add')">
	</div>
</template>

<script>
export default {
	name: 'Home',

	components: {
		BigCard: () => import('../components/BigCard.vue'),
		SmallCard: () => import('../components/SmallCard.vue')
	},

	data () {
		return {
			list: [
				{ id: 1, location: 'Manila, Philippines', temperature: '10', weather: 'Sunny', rangeTemp: [13, 23] },
				{ id: 1, location: 'Manila, Philippines', temperature: '20', weather: 'Sunny', rangeTemp: [13, 23] },
				{ id: 1, location: 'Manila, Philippines', temperature: '30', weather: 'Sunny', rangeTemp: [13, 23] },
				{ id: 1, location: 'Manila, Philippines', temperature: '40', weather: 'Sunny', rangeTemp: [13, 23] },
				{ id: 1, location: 'Manila, Philippines', temperature: '50', weather: 'Sunny', rangeTemp: [13, 23] },
				{ id: 1, location: 'Manila, Philippines', temperature: '25', weather: 'Sunny', rangeTemp: [13, 23] },
				{ id: 1, location: 'Manila, Philippines', temperature: '35', weather: 'Sunny', rangeTemp: [13, 23] },
				{ id: 1, location: 'Manila, Philippines', temperature: '45', weather: 'Sunny', rangeTemp: [13, 23] }
			]
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
