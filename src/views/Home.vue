<template>
	<div class="home">
		<h1>Current Location</h1>
		<BigCard class="big-card-container"/>
        <h2>Other Location</h2>
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
			list: JSON.parse(localStorage.getItem('cities')).reverse()
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
