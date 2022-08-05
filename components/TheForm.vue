<template>
	<form class="form" @submit.prevent>
		<TheInput
			v-model="product.title"
			:type="'text'"
			:name="'product-name'"
			:placeholder="'Введите наименование товара'"
			:className="$v.product.title.$error ? 'invalid' : ''"
			:labelText="'Наименование товара'"
			:functionName="checkValidation"
		/>
		<TheTextarea
			v-model="product.description"
			:name="'product-description'"
			:placeholder="'Введите описание товара'"
			:labelText="'Описание товара'"
		/>
		<TheInput
			v-model="product.url"
			:type="'text'"
			:name="'product-url'"
			:placeholder="'Введите ссылку'"
			:className="$v.product.url.$error ? 'invalid' : ''"
			:labelText="'Ссылка на изображение товара'"
			:functionName="checkValidation"
		/>
		<TheInput
			v-model="product.price"
			:type="'text'"
			:name="'product-price'"
			:placeholder="'Введите цену'"
			:className="$v.product.price.$error ? 'invalid' : ''"
			:maxlength="'15'"
			:labelText="'Цена товара'"
			:functionName="checkValidation"
		/>
		<TheButton
			:text="'Добавить товар'"
			:className="$v.product.$invalid ? '' : 'button--active'"
			:functionName="$v.product.$invalid ? () => {} : createProduct"
		/>
	</form>
</template>

<script>
	import { validationMixin } from 'vuelidate'
	import { required, url } from 'vuelidate/lib/validators'

	export default {
		mixins: [validationMixin],
		data() {
			return {
				product: {
					title: '',
					description: '',
					url: '',
					price: ''
				}
			}
		},
		validations: {
			product: {
				title: { required },
				url: { required, url },
				price: { required },
			}
		},
		methods: {
			createProduct() {
				this.product.id = Date.now();
				this.$emit('create', this.product);
				this.product = {
					title: '',
					description: '',
					url: '',
					type: ''
				}
				this.$v.product.$reset();
			},
			checkValidation(event) {
				const name = event.target.name;

				switch (name) {
					case 'product-name':
						this.$v.product.title.$touch();
						break;
					case 'product-url':
						this.$v.product.url.$touch();
						break;
					case 'product-price':
						this.$v.product.price.$touch();
						break;
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	.form {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		width: 332px;
		height: 440px;
		padding: 24px;
		background: #FFFEFB;
		box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
		border-radius: 4px;
	}
</style>