<template>
	<ul class="products">
		<TheProductCard
			v-for="product in products"
			:key="product.id"
			:product="product"
			@remove="$emit('remove', product)"
		/>
	</ul>
</template>

<script>
	export default {
    props: {
        products: {
            type: Array,
            required: true
        }
    },
	}
</script>

<style lang="scss" scoped>
	.products {
		display: flex;
		flex-wrap: wrap;
		margin: -16px -16px 0 0;

		& div {
			margin: 16px 16px 0 0;
		}
	}
</style>