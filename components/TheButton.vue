<template>
	<button class='button' :class="className" @click="functionName">
		{{ text }}
	</button>
</template>

<script>
export default {
	props: {
		text: {
			type: String,
			default: ''
		},
		className: {
			type: String,
			default: ''
		},
		functionName: {
			type: Function,
			default: () => {}
		}
	}
}
</script>

<style lang="scss" scoped>
.button {
	width: 100%;
	height: 36px;
	background: #EEEEEE;
	box-shadow: none;
	border-radius: 10px;
	border: none;
	font-family: 'Inter', sans-serif;
	color: #B4B4B4;
	font-weight: 600;
	font-size: 12px;
	line-height: 15px;
	cursor: default;

	&--active {
		background: #7BAE73;
		box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
		color: #FFFFFF;
		cursor: pointer;
	}
}
</style>