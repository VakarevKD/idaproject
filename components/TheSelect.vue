<template>
	<div class="select">
	<select 
		:value="value"
		class="select__field"
		@change="changeOption"
	>
		<option
			v-for="option in options"
			:key="option.value"
			:value="option.value"
		>
			{{ option.name }}
		</option>
	</select>
	</div>
</template>

<script>
	export default {
		props: {
			value: {
				type: String,
				default: 'default'
			},
			options: {
				type: Array,
				default: () => []
			}
		},
		methods: {
			changeOption(event) {
				this.$emit('input', event.target.value);
			}
		}
	}
</script>

<style lang="scss" scoped>
	.select {
		display: flex;
		justify-content: end;
		margin-bottom: 16px;

		&__field {
			position: relative;
			display: inline-block;
			width: 120px;
			height: 36px;
			padding: 2px 0 0 15px;
			background: #FFFEFB;
			background-image: url(../images/arrow-down.svg);
			background-repeat: no-repeat;
			background-position: 86% 55%;
			box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
			border-radius: 4px;
			border: none;
			font-weight: 400;
			font-size: 12px;
			line-height: 15px;
			color: #B4B4B4;
			cursor: pointer;
			-moz-appearance: none;
			-webkit-appearance: none;

			&::-ms-expand {
				display: none;
			}
		}
	}
</style>