<template>
	<div class="input">
		<label :for="name" class="input__label">{{ labelText }}<sup class="required"></sup></label>
		<input
			:type="type"
			:name="name"
			:placeholder="placeholder"
			:maxlength="maxlength"
			class="input__field"
			:class="className"
			:value="value"
      @input="changeInput"
			@blur="functionName"
		>
		<p class="invalid--text" :class="className">Поле является обязательным</p>
	</div>
</template>

<script>
export default {
	props: {
		type: {
			type: String,
			default: ''
		},
		name: {
			type: String,
			default: ''
		},
		placeholder: {
			type: String,
			default: ''
		},
		maxlength: {
			type: String,
			default: ''
		},
		labelText: {
			type: String,
			default: ''
		},
		value: {
			type: [String, Number],
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
	},

	methods: {
		changeInput(event) {
			let value;
			if (event.target.name === 'product-price') {
				value = this.correctValue(event.target.value);
			} else {
				value = event.target.value;
			}
			event.target.value = value;
			this.$emit('input', value);
		},
		correctValue(value) {
			const newValue = value.replace(/[^0-9]/g,'').split('');
			switch (newValue.length) {
				case 4:
					newValue.splice(1, 0, ' ');
					break;
				case 5:
					newValue.splice(2, 0, ' ');
					break;
				case 6:
					newValue.splice(3, 0, ' ');
					break;
				case 7:
					newValue.splice(1, 0, ' ');
					newValue.splice(5, 0, ' ');
					break;
				case 8:
					newValue.splice(2, 0, ' ');
					newValue.splice(6, 0, ' ');
					break;
				case 9:
					newValue.splice(3, 0, ' ');
					newValue.splice(7, 0, ' ');
					break;
				case 10:
					newValue.splice(1, 0, ' ');
					newValue.splice(5, 0, ' ');
					newValue.splice(9, 0, ' ');
					break;
				case 11:
					newValue.splice(2, 0, ' ');
					newValue.splice(6, 0, ' ');
					newValue.splice(10, 0, ' ');
					break;
				case 12:
					newValue.splice(3, 0, ' ');
					newValue.splice(7, 0, ' ');
					newValue.splice(11, 0, ' ');
					break;
			}
			value = newValue.join('');
			return value;
		}
	}
}
</script>

<style lang="scss" scoped>
	p {
		display: none;
	}

	.input {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		height: 53px;

		&__label {
			color: #49485E;
			font-weight: 400;
			font-size: 10px;
			line-height: 13px;
		}

		&__field {
			height: 36px;
			padding-left: 16px;
			box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
			border-radius: 4px;
			border: none;
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

	.required::after {
		content: '';
		width: 4px;
		height: 4px;
		background-color: #FF8484;
		display: inline-block;
		border-radius: 50%;
	}

	.invalid {
		display: block;
		border: 1px solid #FF8484;

		&--text {
			font-weight: 400;
			font-size: 8px;
			line-height: 10px;
			letter-spacing: -0.02em;
			color: #FF8484;
			border: none;
		}
	}
</style>