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
		display: flex;
		width: 42px;
		margin: -13%;
		margin-top: -16px;
		background-color: white;
		text-align: left;
		padding: 15px;

		.remove {
			width: 24px;
			height: 22px;
			align-items: baseline;
			margin-top: 24px;
			margin-left: 24px;
			background-color: #3486e6;
			border-radius: 22px;
			color: white;
			border-style: unset;
			cursor: pointer;
		}
		p {
			white-space: break-spaces;
			text-align: center;
			width: 104px;
		}
		.header {
			display: flex;
			flex-direction: row;
			margin-bottom: 20px;
		}
		img {
			width: 42px;
			background: none;
			transform: translate(7px, -13px);
		}
	}
	@media (max-width: 426px) {
		.cart-item-card {
			img {
				width: 42px;
				transform: translate(18px, -13px);
			}
		}
	}
	@media (max-width: 426px) {
		.cart-item-card {
			padding-left: 0;
			.header {
				width: 90%;
				margin-left: 42px;
			}
			img {
				display: none;
			}
		}
	}
</style>
