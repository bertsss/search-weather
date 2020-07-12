<template>
	<div class="big-card">
		<span>{{ location }}</span>

		<div class="temp-container">
			<img :src="require('@/assets/sunny.png')" />
			<p>{{ temp }}°C</p>
		</div>

		<div class="weather-container">
			<p class="weather">{{ weather }}</p>
			<p class="temp">{{ range }}</p>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		location: {
			type: String,
			default: 'Manila, Philippines'
		},

		temp: {
			type: String,
			default: '10'
		},

		weather: {
			type: String,
			default: 'Sunny'
		},

		rangeTemp: {
			type: Array,
			default: () => [13, 22]
		}
	},

	computed: {
		range () {
			return `${this.rangeTemp[0]}° - ${this.rangeTemp[1]}°`
		}
	}
}
</script>

<style lang="scss" scoped>
.big-card {
	background-color: #ffffff;
	border-radius: 10px;
	box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
	width: 450px;
	box-shadow: 5px black;
	padding: 20px 40px;

	span {
		font-size: 18px;
		font-weight: 400;
	}

	.temp-container {
		margin: 20px 0px;
		display: flex;
		align-items: center;

		img {
			width: 100px;
			height: 100px;
		}

		p {
			font-size: 38px;
			margin-left: auto;
		}
	}

	.weather {
        font-weight: 100;
		font-size: 18px;
		color: #0ba399;
		margin-bottom: 5px;
	}

	.temp {
		font-size: 10px;
	}
}

@media only screen and (max-width: 600px) {
    .big-card {
        width: 350px;
    }
}
</style>
