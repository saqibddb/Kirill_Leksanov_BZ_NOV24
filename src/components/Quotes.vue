<template>
	<div class="quotes">
		<div class="header">
			<h1 class="title"><img :src="umbrellaSmall" /> Umbrella Hub</h1>
			<img 
				:src="close" 
				class="close" 
				@click="$emit('close-quotes')" />
		</div>
		<img :src="wind" class="wind"/>
		<div v-if="loading" class="loading-message">{{ message }}</div>
		<div v-else>
			<div class="landing__text">
				<h1 class="title">Fast like the wind!</h1>
				<h3 class="subtitle">We dove deep through the internet to get you these great quotes</h3>
			</div>
			<div class="quotes-list">
				<div v-for="quote in quotes" :key="quote.id" class="quote">
					<img :src="getLogos(quote.id)" class="logo" />
					<img :src="getRatings(quote.id)" class="rating" />
					<h1 class="monthly">{{ quote.monthly }}<span class="month-suffix">/mo</span></h1>
					<h3 class="annually">{{ quote.annually }}<span class="annual-suffix"> per year</span></h3>
					<!-- <button class="buy-now">Buy Now</button> -->
					<Button :text="'Buy Now'" />
				</div>
			</div>
			<div class="summary">
				<h1 class="summary__title">Your summary: </h1>
				<p class="summary__description">
					<span class="highlight">{{ companyName }}</span> is interested in purchasing <span class="highlight">{{ insuranceType }}</span>.
				</p>
				<p class="summary__description">
					<span>{{ companyName }}</span> can be reached at <br/><span class="highlight">{{ phoneNumber }}</span>.
				</p>
			</div>
		</div>
	</div>
</template>

<script>
import Wind from '@/assets/wind.svg';
import Close from '@/assets/close.svg'
import UmbrellaSmall from '@/assets/umbrella-small.svg'
import Progressive from '@/assets/progressive.png';
import Geico from '@/assets/geico.png';
import StateFarm from '@/assets/state-farm.png';
import ProgressiveRatings from '@/assets/progressive-ratings.svg';
import GeicoRatings from '@/assets/geico-ratings.svg';
import StateFarmRatings from '@/assets/state-farm-ratings.svg';

import Button from '@/components/ButtonComponent.vue';

export default {
	components: {
		Button
	},
	mounted() {
		this.loading = true;
		this.cycleMessages();
		window.setTimeout(() => {
			this.loading = false
		}, 8300)
	},
	props: {
		companyName: {
			type: String,
			required: true
		},
		insuranceType: {
			type: String,
			required: true
		},
		phoneNumber: {
			type: String,
			required: true
		}
	},
	methods: {
		cycleMessages() {
			const messages = [
				'Searching the internet for quotes',
				'Proving P=NP...',
				'Doing the heavy lifting',
				'Generating witty dialog...'
			];
			const delayLoop = () => {
				return (m, i) => {
					setTimeout(() => {
						this.message = m;
					}, i * 2000);
				}
			};
			messages.forEach(delayLoop());
		},
		getLogos(quote) {
			if (quote == 1) {
				return this.progressive;
			} else if (quote == 2) {
				return this.geico;
			} else if (quote == 3) {
				return this.stateFarm;
			}
			return null
		},
		getRatings(quote) {
			if (quote == 1) {
				return this.progressiveRatings;
			} else if (quote == 2) {
				return this.geicoRatings;
			} else if (quote == 3) {
				return this.stateFarmRatings;
			}
			return null
		},
		
	},
	data() {
		return {
			loading: null,
			message: null,
			wind: Wind,
			close: Close,
			umbrellaSmall: UmbrellaSmall,
			progressive: Progressive,
			geico: Geico,
			stateFarm: StateFarm,
			progressiveRatings: ProgressiveRatings,
			geicoRatings: GeicoRatings,
			stateFarmRatings: StateFarmRatings,
			quotes: [
				{
					id: 1,
					monthly: '$120',
					annually: '$1440'
				},
				{
					id: 2,
					monthly: '$125',
					annually: '$1500'
				},
				{
					id: 3,
					monthly: '$125',
					annually: '$1500'
				},

			]
		}
	}
}
</script>

<style lang="scss" scoped>
	.quotes {
		background: white;
		height: 100vh;
		left: 0;
		position: absolute;
		top: 0;
		width: 100vw;
		z-index: 99;
		padding: 40px 32px 0;
		& .header {
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			align-items: center;
			& .title {
				font-size: 14.4471px;
				line-height: 17px;
				color: var(--primary);
				display: flex;
				align-items: center;
				font-weight: normal;
				& img {
					margin-right: 8.63px;
				}
			}
		}
		& .wind {
			margin: 61px auto 45px;
			display: block;
		}
		
		& .loading-message {
			font-size: 24px;
			line-height: 30px;
			color: var(--typeface);
			font-weight: bold;
			text-align: center;
		}
		& .landing__text {
			& .title {
				color: var(--typeface);
				font-size: 38px;
				font-weight: bold;
				line-height: 45px;
				text-align: center;
				&.loading-message {
					font-size: 24px;
					line-height: 30px;
				}
			}
			& .subtitle {
				color: var(--typeface);
				font-size: 20px;
				font-weight: normal;
				line-height: 23px;
				margin: 15px auto 60px;
				text-align: center;
			}
		}
		& .quotes-list {
			display: flex;
			flex-direction: column;
			& .quote {
				background: #FFFFFF;
				border: 1px solid #BDBDBD;
				box-sizing: border-box;
				box-shadow: var(--box-shadow);
				border-radius: 4px;
				padding: 35px 23px;
				margin-bottom: 30px;
				display: flex;
				flex-direction: column;
				align-items: center;
				& .logo {
					margin-bottom: 20.71px;
				}
				& .rating {
					margin-bottom: 60px;
				}
				& .monthly {
					font-weight: bold;
					font-size: 42px;
					line-height: 49px;
					color: var(--typeface);
					margin-bottom: 8px;
					& .month-suffix {
						font-weight: normal;
						font-size: 24px;
						color: var(--typeface);
					}
				}
				& .annually {
					font-weight: 500;
					font-size: 16.2556px;
					line-height: 19px;
					color: var(--gray-3);
					margin-bottom: 60px;
				}
				& .buy-now {
					background: #71F79F;
					border-radius: 8px;
					box-shadow: var(--box-shadow);
					color: var(--typeface);
					font-size: 18px;
					font-weight: bold;
					line-height: 21px;
					padding: 14px 0;
					text-align: center;
					text-transform: uppercase;
					width: 100%;
				}
				&:first-child {
					border: 2px solid var(--primary);
				}
			}
		}
		& .summary {
			margin-top: 20px;
			margin-bottom: 50px;
			& .summary__title {
				font-weight: 500;
				font-size: 20px;
				line-height: 23px;
				color: var(--typeface);
				margin-bottom: 22px;
			}
			& .summary__description {
				font-size: 16px;
				line-height: 19px;
				color: var(--typeface);
				margin-bottom: 16px;
				& .highlight {
					font-weight: 500;
					color: var(--primary);
					text-decoration-line: underline;
				}
			}
		}
	}
</style>