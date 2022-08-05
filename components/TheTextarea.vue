<template>
	<div class="textarea">
		<label :for="name" class="textarea__label">{{ labelText }}</label>
		<textarea
			:name="name"
			:placeholder="placeholder"
			class="textarea__field"
			:value="value"
      @input="input"
		></textarea>
	</div>
</template>

<script>

export default {
	props: {
		name: {
			type: String,
			default: ''
		},
		placeholder: {
			type: String,
			default: ''
		},
		labelText: {
			type: String,
			default: ''
		},
		value: {
			type: String,
			default: ''
		}
	},

	methods: {
		input(e) {
			const value = e.target.value;
			this.$emit('input', value);
		}
	}
}
</script>

<style lang="scss" scoped>
	.textarea {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		height: 125px;

		&__label {
			color: #49485E;
			font-weight: 400;
			font-size: 10px;
			line-height: 13px;
		}

		&__field {
			height: 108px;
			padding: 10px 0 0 16px;
			box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
			border-radius: 4px;
			border: none;
			resize: none;
			font-weight: 400;
			font-size: 12px;
			line-height: 15px;

			&:hover {
				box-shadow: 0px 5px 10px 0px rgb(9, 255, 5, 0.5);
			}

			&:focus {
				box-shadow: 0px 5px 10px 0px rgb(9, 255, 5, 0.5);
			}

			&::placeholder {
				color: #B4B4B4;
			}
		}
	}
</style>