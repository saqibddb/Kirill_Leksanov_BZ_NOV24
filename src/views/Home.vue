<template>
	<div class="home">
		<div class="landing">
			<img :src="umbrellaLogo" class="landing__logo" />
			<h1 class="landing__heading">So what gives?</h1>
			<div class="landing__list">
				<div class="landing__list-item">
					<h3 class="pointer">1</h3>
					<div class="text">Answer a few simple questions about your business</div>
				</div>
				<div class="landing__list-item">
					<h3 class="pointer">2</h3>
					<div class="text">Browse through specially curated quotes</div>
				</div>
				<div class="landing__list-item">
					<h3 class="pointer">3</h3>
					<div class="text">Select your quote-of-choice and receive your policy instantly</div>
				</div>
			</div>
			<Button 
				@clicked="getStarted" 
				:text="'Get Started'" 
				class="get-started"/>
			<div class="powered-by"><img :src="zap" class="zap" /> Powered by Briza</div>
		</div>
		<Stepper
			v-if="started" 
			@close-stepper="started = false" 
			@get-quotes="fetchQuotes" />
		<Quotes
			v-if="getQuotes" 
			@close-quotes="getQuotes = false"
			:companyName="companyName" 
			:insuranceType="insuranceType" 
			:phoneNumber="phoneNumber" />
	</div>
</template>

<script>

import Button from '@/components/ButtonComponent.vue'
import Quotes from '@/components/Quotes.vue'
import Stepper from '@/components/Stepper.vue'

import UmbrellaLogo from '@/assets/umbrella-logo.svg'
import Zap from '@/assets/zap.svg'

export default {
	components: {
		Button,
		Quotes,
		Stepper
	},
	methods: {
		getStarted() {
			this.started = true;
		},
		fetchQuotes(payload) {
			const { companyName, insuranceType, phoneNumber } = payload;
			this.started = false;
			this.companyName = companyName;
			this.insuranceType = insuranceType;
			this.phoneNumber = phoneNumber;
			this.getQuotes = true;
		}
	},
	data() {
		return {
			companyName: null,
			getQuotes: false,
			insuranceType: null,
			phoneNumber: null,
			started: false,
			umbrellaLogo: UmbrellaLogo,
			zap: Zap
		}
	}
}
</script>

<style lang="scss" scoped>
	.home {
		font-family: 'Roboto';
		padding: 0 34px;
		& .landing {
			display: flex;
			flex-direction: column;
			justify-content: center;
			margin-top: 126px;
			& .landing__heading {
				color: var(--typeface);
				font-size: 40px;
				font-weight: bold;
				line-height: 47px;
				margin-top: 47px;
				text-align: center;
			}
			& .landing__list {
				display: flex;
				flex-direction: column;
				margin-top: 60px;
				& .landing__list-item {
					align-items: center;
					display: flex;
					flex-direction: row;
					margin-bottom: 23px;
					&:last-child {
						margin-bottom: 0;
					}
					& .pointer {
						align-items: center;
						background: var(--secondary);
						border-radius: 50%;
						color: var(--primary);
						display: flex;
						flex-direction: row;
						height: 36px;
						justify-content: center;
						position: absolute;
						width: 36px;
					}
					& .text {
						color: var(--typeface);
						font-size: 18px;
						margin-left: 54px;
					}
				}
			}
			& .get-started {
				margin-top: 70px;
			}
			& .powered-by {
				color: var(--gray-4);
				display: flex;
				flex-direction: row;
				justify-content: center;
				margin-top: 60px;
				& .zap {
					margin-right: 7px;
				}
			}
		}
	}
	
</style>