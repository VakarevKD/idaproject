<template>
  <div class="page container">
		<section class="sidebar">
			<h2 class="sidebar__title">Добавление товара</h2>
			<div class="sidebar__form-wrapper">
				<TheForm 
					@create="createProduct"
				/>
			</div>
		</section>
		<section class="products">
			<TheSelect
				v-model="selectedSort"
				:options="sortOptions"
			/>
			<TheProductsList 
				:products="products"
				@remove="removeProduct"
			/>
		</section>
	</div>
</template>

<script>
	export default {
		name: "IndexPage",

		data() {
			return {
				products: [],
				selectedSort: 'default',
				sortOptions: [
					{value: 'default', name: 'По умолчанию'},
					{value: 'price-max', name: 'По цене вверх'},
					{value: 'price-min', name: 'По цене вниз'},
					{value: 'name', name: 'По имени'}
				]
			}
		},

		watch: {
			selectedSort(newValue) {
				this.sortProducts(newValue);
			}
		},
		mounted() {
			if (localStorage.products) {
				this.products = JSON.parse(localStorage.getItem('products'));
				this.sortProducts(this.selectedSort);
			}
		},
		methods: {
			createProduct(product) {
				this.products.push(product);
				this.sortProducts(this.selectedSort);
				localStorage.setItem('products', JSON.stringify(this.products));
			},
			removeProduct(product) {
				this.products = this.products.filter(el => el.id !== product.id);
				localStorage.setItem('products', JSON.stringify(this.products));
			},
			sortProducts(selectedSort) {
				const products = this.products;
				switch(selectedSort) {
					case 'default':
						products.sort((product1, product2) => product1.id > product2.id ? 1 : -1);
						break;
					case 'price-max':
						products.sort((product1, product2) => parseInt(product1.price.split(' ').join('')) > parseInt(product2.price.split(' ').join('')) ? 1 : -1);
						break;
					case 'price-min':
						products.sort((product1, product2) => parseInt(product1.price.split(' ').join('')) < parseInt(product2.price.split(' ').join('')) ? 1 : -1);
						break;
					case 'name':
						products.sort((product1, product2) => product1.title > product2.title ? 1 : -1);
						break;
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	.page {
		margin-top: 32px;
	}

	.container {
		display: grid;
		grid-template-columns: 1fr 3fr;
		column-gap: 16px;
	}	

	.sidebar {

		&__form-wrapper {
			position: sticky;
			top: 24px;
		}

		&__title {
			margin-bottom: 16px;
			font-weight: 600;
			font-size: 28px;
			line-height: 35px;
			color: #3F3F3F;
		}
	}
</style>
