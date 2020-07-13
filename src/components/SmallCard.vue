<template>
	<div class="small-card" @click="$emit('click', location)">
		<span>{{ location }}</span>

		<div class="temp-container">
			<img :src="require('@/assets/sunny.png')" />
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
        }

        .temp {
            font-size: 8px;
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
