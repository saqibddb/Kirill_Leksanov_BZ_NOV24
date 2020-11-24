<template>
	<div class="stepper">
		<div class="header">
			<h1 class="title"><img :src="umbrellaSmall" /> Umbrella Hub</h1>
			<img 
				:src="close" 
				class="close" 
				@click="$emit('close-stepper')" />
		</div>
		<div 
			class="step step-1" 
			:class="{ disabled: this.step !== 1, invisible: this.step >= 2}">
			<div class="step__heading">
				<h3 class="pointer">1</h3> 
				<div class="text">What type of insurance are you looking for?</div>
			</div>
			<div class="chips-list">
				<div 
					v-for="(option) in stepOneOptions" 
					:key="option.id" 
					:class="{ first: option.id == 1, selectedOption: option.title == stepOneOption}" 
					@click="stepOne(option.title)"
					class="chip">
					<img :src="getIcon(option.id)" class="icon" />
					<div class="text">
						<h1>{{ option.title }}</h1>
						<h2>{{ option.subtitle }}</h2>
					</div>
				</div>
			</div>
		</div>
		<div
			class="step step-2" 
			:class="{ disabled: this.step !== 2, invisible: this.step >= 3}">
			<div class="step__heading">
				<h3 class="pointer">2</h3> 
				<div class="text">What’s the name of your business?</div>
			</div>
			<div class="form">
				<input 
					v-model="companyName" 
					:class="{ error: companyNameError }" 
					type="tel" 
					class="input" 
					placeholder="Business Name" />
				<small v-if="companyNameError" class="error-message">{{ companyNameError }}</small>
				<button @click="validateCompanyName" class="submit">OK <img :src="check" /></button>
			</div>
		</div>
		<div
			class="step step-3" 
			:class="{ disabled: this.step !== 3,  invisible: this.step >= 4}">
			<div class="step__heading">
				<h3 class="pointer">3</h3> 
				<div class="text">What’s the phone number?</div>
			</div>
			<div class="form">
				<input 
					v-model="phoneNumber" 
					:class="{ error: phoneNumberError }" 
					type="text" 
					class="input" 
					placeholder="111-111-1111" />
				<small v-if="phoneNumberError" class="error-message">{{ phoneNumberError }}</small>
				<Button 
					@clicked="validatePhoneNumber" 
					:text="'Get Quotes'"
					class="get-quotes" />
			</div>
		</div>
		<div class="footer">
			<div class="step-counter">{{ step }}/{{ steps}}</div>
			<div class="controls">
				<button @click="decrementStep" class="control up" :class="{ disabled: step == 1}">
					<img :src="chevronUp" />
				</button>
				<button @click="incrementStep" class="control down"  :class="{ disabled: step == 3}">
					<img :src="chevronDown" />
				</button>
			</div>
		</div>
	</div>
</template>

<script>
import Button from '@/components/ButtonComponent.vue';

import BriefCase from '@/assets/briefcase.svg'
import Check from '@/assets/check.svg'
import Close from '@/assets/close.svg'
import ChevronUp from '@/assets/chevron-up.svg'
import ChevronDown from '@/assets/chevron-down.svg'
import Cloud from '@/assets/cloud.svg'
import Cyber from '@/assets/cyber.svg'
import Package from '@/assets/package.svg'
import UmbrellaSmall from '@/assets/umbrella-small.svg'

export default {
	components: {
		Button
	},
	methods: {
		closeStepper() {
			this.$root.stepperOpen = false;
		},
		decrementStep() {
			if (this.step >= 2) {
				this.step--;
			}
			return null
		},
		getIcon(option) {
			if (option == 1) {
				return this.briefCase;
			} else if (option == 2) {
				return this.cloud;
			} else if (option == 3) {
				return this.packageIcon;
			} else if (option == 4) {
				return this.cyber;
			}
			return null
		},
		incrementStep() {
			if (this.step <= 2) {
				this.step++;
			}
			return null
		},
		stepOne(option) {
			this.step++;
			this.stepOneOption = option;
			return null
		},
		validateCompanyName() {
			if (this.companyName.length >= 1) {
				this.step++;
				this.companyNameError = null;
			} else {
				this.companyNameError = 'Invalid business name.'
			}
			return null
		},
		validatePhoneNumber() {
			if (this.phoneNumber.length >= 1 && this.phoneNumber.length == 12) {
				this.phoneNumberError = null;
				this.$emit('get-quotes', { companyName: this.companyName, insuranceType: this.stepOneOption, phoneNumber: this.phoneNumber });
			} else {
				this.phoneNumberError = 'Invalid phone number.'
			}
			return null
		},
	},
	data() {
		return {
			briefCase: BriefCase,
			check: Check,
			chevronDown: ChevronDown,
			chevronUp: ChevronUp,
			close: Close,
			cloud: Cloud,
			companyName: '',
			companyNameError: null,
			cyber: Cyber,
			packageIcon: Package, // package is a reserved word
			phoneNumber: '',
			phoneNumberError: null,
			step: 1,
			stepOneOption: null,
			stepOneOptions: [
				{
					id: 1,
					title: "Professional Liability",
					subtitle: "Erros & Omissions (E&O insurance)"
				},
				{
					id: 2,
					title: "General Liability",
					subtitle: "Help mitigate against loss (CGL insurance)"
				},
				{
					id: 3,
					title: "Business Owner’s Policy",
					subtitle: "The complete package (BOP)"
				},
				{
					id: 4,
					title: "Cyber",
					subtitle: "Internet-based risks (CLIC)"
				},
			],
			steps: 3,
			umbrellaSmall: UmbrellaSmall,
		}
	}
}
</script>

<style lang="scss" scoped>
	.stepper {
		background: white;
		height: 100vh;
		left: 0;
		padding: 40px 34px 0;
		position: absolute;
		top: 0;
		width: 100vw;
		z-index: 99;
		overflow: hidden;
		& .header {
			align-items: center;
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			& .title {
				align-items: center;
				color: var(--primary);
				display: flex;
				font-size: 14.4471px;
				font-weight: normal;
				line-height: 17px;
				& img {
					margin-right: 8.63px;
				}
			}
		}
		& .step {
			display: block;
			margin-bottom: 10px;
			margin-top: 40px;
			&.disabled {
				opacity: 0.1;
			}
			&.invisible {
				display: none;
			}
			& .step__heading {
				align-items: center;
				color: var(--typeface);
				display: flex;
				font-size: 24px;
				font-weight: bold;
				line-height: 28px;
				& .pointer {
					align-items: center;
					background: var(--secondary);
					border-radius: 50%;
					color: var(--primary);
					display: flex;
					flex-direction: row;
					font-size: 18px;
					font-weight: bold;
					height: 36px;
					justify-content: center;
					line-height: 21px;
					position: absolute;
					width: 36px;
				}
				& .text {
					color: var(--typeface);
					font-size: 24px;
					font-weight: bold;
					line-height: 28px;
					margin-left: 57px;
				}
			}
			&.step-1 {
				& .chips-list {
					display: flex;
					flex-direction: column;
					& .chip {
						align-items: center;
						background: #FFFFFF;
						border-radius: 4px;
						border: 1px solid #BDBDBD;
						box-shadow: var(--box-shadow);
						box-sizing: border-box;
						display: flex;
						flex-direction: row;
						margin-top: 20px;
						padding: 20px 0;
						&.first {
							margin-top: 40px;
						}
						&.selectedOption {
							background: var(--secondary);
						}
						& .icon {
							margin-left: 20px;
						}
						& .text {
							margin-left: 15px;
							& h1 {
								color: var(--typeface);
								font-size: 17.0345px;
								font-weight: 500;
								line-height: 20px;
							}
							& h2 {
								color: var(--typeface);
								font-size: 12px;
								font-weight: normal;
								line-height: 14px;
							}
						}
					}
				}
			}
			& .form {
				display: flex;
				flex-direction: column;
				margin-top: 40px;
				& .input {
					border-bottom: 1px solid black;
					color: var(--primary);
					font-size: 20px;
					font-weight: normal;
					line-height: 23px;
					padding-bottom: 7px;
					&.error {
						border-color: red;
					}
					&:focus,
					&:active {
						outline: none;
					}
				}
				& .error-message {
					color: red;
					font-weight: bold;
					padding-top: 4px;
				}
				& .submit {
					align-items: center;
					background: var(--secondary);
					border-radius: 8px;
					box-shadow: var(--box-shadow);
					color: var(--primary);
					display: flex;
					flex-direction: row;
					font-size: 18px;
					font-weight: 500;
					height: 50px;
					justify-content: space-around;
					letter-spacing: 0.2px;
					line-height: 21px;
					margin-top: 20px;
					padding: 15px 17px;
					text-align: center;
					width: 96px;
					&:disabled {
						opacity: 0.4;
					}
					&.check {
						padding-left: 12.25px;
						& .v-icon__svg {
							fill: var(--primary);
						}
					}
				}
			}
			& .get-quotes {
				margin-top: 70px;
			}
		}
		& .footer {
			align-items: center;
			background: var(--primary);
			bottom: 0;
			box-shadow: 0px -1px 4px rgba(0, 0, 0, 0.25);
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			margin-left: -34px;
			padding: 20px 28px;
			position: fixed;
			width: 100vw;
			& .step-counter {
				color: #FFFFFF;
				font-size: 18px;
				font-weight: bold;
				line-height: 21px;
			}
			& .controls {
				display: flex;
				flex-direction: row;
				& .control {
					align-items: center;
					background: white;
					display: flex;
					flex-direction: row;
					height: 36px;
					justify-content: center;
					width: 36px;
					&.up {
						margin-right: 8.42px;
					}
					&.disabled {
						opacity: 0.8;
					}
				}
			}
		}
	}
</style>
