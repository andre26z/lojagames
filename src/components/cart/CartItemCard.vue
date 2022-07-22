<template>
	<div class="cart-item-card">
		<div class="header">
			<div class="image">
				<img :src="item.image" alt="" />
			</div>
			<p>{{ item.name }}</p>
			<p>Quantidade: {{ item.quantity }}</p>
			<p>Valor Total: R${{ item_cost.toFixed(2) }}</p>
			<button class="remove" @click.prevent="removeFromCart()">X</button>
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
		methods: {
			removeFromCart() {
				this.$store.commit("removeFromCart", this.item);
			},
		},
	};
</script>

<style lang="scss">
	.cart-item-card {
		width: 42px;
		margin: -13%;
		margin-top: -16px;
		background-color: white;
		text-align: left;
		padding: 15px;
		justify-content: space-between;
		.remove {
			width: 24px;
			height: 22px;
			align-items: baseline;
			margin-top: 24px;
			margin-left: 24px;
			background-color: #3486e6;
			border-radius: 12px;
			color: white;
			border-style: unset;
			cursor: pointer;
		}
		p {
			white-space: break-spaces;
			text-align: center;
		}
		.header {
			display: flex;
			flex-direction: row;
		}
		img {
			width: 42px;
			background: none;
		}
	}
</style>
