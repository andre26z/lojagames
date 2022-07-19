<template>
	<div class="cart-item-card">
		<div class="header">
			<div class="image">
				<img :src="item.image" alt="" />
			</div>
			<h3>{{ item.name }}</h3>
			<h4>Quantidade: {{ item.quantity }}</h4>
			<h4>Valor Total: R${{ item_cost.toFixed(2) }}</h4>
		</div>

		<!-- <p>{{ description }}</p> -->
	</div>
</template>

<script>
	export default {
		props: ["item"],
		computed: {
			item_cost() {
				return this.item.price * this.item.quantity;
			},
		},
	};
</script>

<style lang="scss" scoped>
	.cart-item-card {
		width: 90%;
		height: 100px;
		margin: 5%;
		background-color: white;
		padding: 10px;
		text-align: left;

		.header {
			display: flex;
			justify-content: space-around;
		}
	}
</style>
