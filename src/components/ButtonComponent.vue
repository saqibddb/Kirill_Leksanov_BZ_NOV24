<template>
	<button @click="$emit('clicked')">{{ text }}</button>
</template>

<script>
export default {
	props: {
		text: {
			type: String,
			required: true
		}
	}
}
</script>

<style lang="scss" scoped>
	button {
		background: var(--success);
		border-radius: 8px;
		box-shadow: var(--box-shadow);
		color: var(--typeface);;
		font-size: 18px;
		font-weight: bold;
		line-height: 21px;
		padding: 14px 0;
		text-align: center;
		text-transform: uppercase;
		width: 100%;
		&:focus,
		&:active {
			border: none;
			outline: none;
		}
	}
</style>