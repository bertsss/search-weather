<template>
	<div class="small-card" @click="isClickable ? $emit('click', location): ''">
		<span>{{isClickable ? location : date }}</span>

		<div class="temp-container">
			<img :src="`http://openweathermap.org/img/wn/${icon}.png`" :alt="weather" />
            <div class="weather-container">
                <p class="weather">{{ weather }}</p>
                <p class="temp">{{ range }}</p>
            </div>
			<p>{{ temp }}°C</p>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		date: {
			type: String,
			default: new Date().toDateString()
		},

		location: {
			type: String,
			default: 'Manila, Philippines'
		},

		weather: {
			type: String,
			default: 'Sunny'
		},

		temp: {
			type: Number
		},

		rangeTemp: {
			type: Array,
			default: () => [13, 22]
		},

		icon: {
			type: String
		},

		isClickable: {
			type: Boolean,
			default: false
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
.small-card {
	background-color: #ffffff;
	border-radius: 10px;
	box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
	width: 450px;
	box-shadow: 5px black;
	padding: 20px;

	span {
		font-size: 16px;
        font-weight: 400;
	}

	.temp-container {
		margin-top: 20px;
		display: flex;
        align-items: center;

        .weather {
            font-weight: 400;
            font-size: 14px;
            color: #0ba399;
            margin-bottom: 5px;
            text-transform: capitalize;
        }

        .temp {
            font-size: 10px;
            text-align: left;
        }

		img {
            margin-right: 15px;
			width: 50px;
			height: 50px;
		}

		p {
			font-size: 26px;
			margin-left: auto;
		}
	}
}

@media only screen and (max-width: 600px) {
    .small-card {
        width: 350px;
    }
}
</style>
