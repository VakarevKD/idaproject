<template>
	<div class="product">
		<button class="product__delete" @click="$emit('remove', product)"></button>
		<img class="product__img" width=332 height=220 :src="product.url" alt="product">
		<div class="product__body">
			<p class="product__title">{{ product.title }}</p>
			<p class="product__description">{{ product.description }}</p>
			<p class="product__price">{{ product.price }} руб.</p>
		</div>
	</div>
</template>

<script>
	export default {
		props: {
			product: {
				type: Object,
				required: true
			}
		}
	}
</script>

<style lang="scss" scoped>
	.product {
		position: relative;
		width: 332px;
		height: 440px;
		box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
		border-radius: 4px;
		background: #FFFEFB;
		cursor: pointer;

		&__delete {
			display: none;
			position: absolute;
			width: 32px;
			height: 32px;
			top: -10px;
			right: -7px;
			background-image: url('../images/delete-button.svg');
			background-repeat: no-repeat;
			background-size: 16px;
			background-position: center;
			background-color: #FF8484;
			box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
			border-radius: 10px;
			border: none;
			cursor: pointer;
		}

		&__img {
			border-radius: 4px 4px 0 0;
		}

		&__body {
			padding: 10px 16px 24px;
		}

		&__title {
			margin-bottom: 16px;
			font-weight: 600;
			font-size: 20px;
			line-height: 25px;
		}

		&__description {
			margin-bottom: 32px;
			height: 80px;
			overflow-y: auto;
			font-weight: 400;
			font-size: 16px;
			line-height: 20px;
		}

		&__price {
			font-weight: 600;
			font-size: 24px;
			line-height: 30px;
		}

		&:hover .product__delete {
			display: inline-block;
		}
	}
</style>