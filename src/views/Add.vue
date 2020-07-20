<template>
	<div class="add">
		<img
			:src="require('@/assets/close.png')"
			@click="$router.push('/')"
		>
		<h1>Add new location </h1>
		<h4>Find a city and tap on it to add</h4>
		<input
			type="text"
			placeholder="Start typing here..."
			v-model="text"
			@input="search"
		>

		<Loading
			v-if="loading"
			class="loading"
		/>

		<div v-else>
			<div v-if="list.length">
				<div
					v-for="(item, key) in list"
					class="country-container"
					@click="$router.push('/')"
					:key="key"
				>
					<p class="country">{{ item.countryCode }}</p>
					<p class="city">{{ item.city }}</p>
				</div>

			</div>
			<div v-if="text && !list.length">
				<h3>No results found</h3>
			</div>
		</div>

	</div>
</template>

<script>
export default {
	name: 'Add',

	components: {
		Loading: () => import('../components/Loading.vue')
	},

	data () {
		return {
			text: '',
			loading: false,
			list: []
		}
	},

	methods: {
		search () {
			if (this.text) {
				this.loading = true
				if (this.timeout) clearTimeout(this.timeout)
				this.timeout = setTimeout(async () => {
					await fetch(`https://wft-geo-db.p.rapidapi.com/v1/geo/cities?namePrefix=${this.text}`, {
						method: 'GET',
						headers: {
							'x-rapidapi-host': 'wft-geo-db.p.rapidapi.com',
							'x-rapidapi-key': '4efb42ea59mshc60e51b3f527ba8p1f76cbjsnd04f08ccbac5'
						}
					}).then(res => res.json()).then(data => {
						this.list = data.data
					}).catch(err => {
						console.log(err)
					})
					this.loading = false
				}, 500)
			}
		}

		// select (city) {
		// 	const cities = JSON.parse(localStorage.getItem('cities'))
		// 	if (cities) {
		// 		if (cities.length === 5) cities.shift()
		// 		cities.push(city)
		// 		localStorage.setItem('cities', JSON.stringify(cities))
		// 	} else {
		// 		localStorage.setItem('cities', JSON.stringify([city]))
		// 	}
		// 	this.$router.push('/')
		// }
	}
}
</script>

<style lang="scss" scoped>
.add {
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

	input {
		font-family: "Montserrat", sans-serif;
		color: #606060;
		height: 40px;
		border: 0;
		outline: 0;
		border-bottom: 2px solid #000000;
		background-color: #f5f5f5;
		width: 450px;
		margin-bottom: 30px;
	}

	.loading {
		margin: 0px auto;
	}

	.country-container {
		display: flex;
		flex-direction: column;

		background-color: #ffffff;
		border-radius: 10px;
		box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
		width: 450px;
		box-shadow: 5px black;
		padding: 10px;
		font-size: 16px;
		margin-bottom: 20px;
		cursor: pointer;

		&:hover {
			background-color: #60d8d0;

			p {
				color: #ffffff;
			}
		}

		.country {
			font-weight: 700;
			margin-bottom: 5px;
		}

		.city {
			color: #0ba399;
		}
	}
}

@media only screen and (max-width: 600px) {
	.add {
		.country-container,
		input {
			width: 350px;
		}
	}
}
</style>
