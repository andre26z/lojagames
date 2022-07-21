<template>
	
	<div>
		<div v-for="item in items" :key="item.id" :item="item" />
			<p>Valor Total: R$ {{ cart_total.toFixed(2) }}</p>
	</div>
</template>

<script>
	
	export default {
		
		props: ["products"],
		computed: {
			items() {
				return this.$store.getters.cartItems;
			},
			cart_total() {
				return this.$store.getters.cartItems.reduce(
					(a, b) => a + b.price * b.quantity,
					0
				);
			},
			
		},
	};
</script>

<style lang="scss" scoped>
	.cart-item-card {
		position: absolute;
		display: inline-flex;
		flex-direction: column;
		width: 262px;
		height: 325px;
		justify-content: center;
		align-items: center;
		border: black solid 1px;
		float: right;
	}
	img {
		width: 30%;
	}
</style>
