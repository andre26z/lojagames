<template>
	<div class="drawer" :class="{ show: active.product_drawer }">
		<cart-item-card v-for="item in items" :key="item.id" :item="item">
		</cart-item-card>
		<div class="cart-total" v-if="product_total">
			<p>Frete: {{ frete_total.toFixed(2) }}</p>
			<p>
				<strong> Total: R$ {{ cart_total.toFixed(2) }} </strong>
			</p>
			<button class="finalizarcompra">FINALIZAR COMPRA</button>
		</div>
	</div>
</template>

<script>
	import CartSummaryPaymentCard from "../cart/CartSummaryPaymentCard.vue";
	import CartItemCard from "../cart/CartItemCard.vue";
	export default {
		components: {
			CartSummaryPaymentCard,
			CartItemCard,
		},

		props: ["product", "active"],

		emits: ["closeProductDrawer"],

		data() {
			return {
				frete: 10,
			};
		},
		methods: {
			addToCart() {
				this.$store.commit("addToCart", this.product);
			},
			removeFromCart() {
				this.$store.commit("removeFromCart", this.product);
			},
		},
		computed: {
			cart_total() {
				return this.$store.getters.cartItems.reduce(
					(a, b) => a + b.price * b.quantity,
					0
				);
			},
			product_total() {
				return this.$store.getters.productQuantity(this.product);
			},
			items() {
				return this.$store.getters.cartItems;
			},

			frete_total() {
				if (this.cart_total > 250) {
					return (this.cart_total = 0);
				} else {
					return this.frete;
				}
			},
		},
	};
</script>

<style lang="scss" scoped>
	.drawer-background {
		position: fixed;
		left: 0;
		top: 0;
		z-index: 100;
		display: flex;
		transition: display 0.5s;
		&.show {
			display: block;
		}
	}
	.drawer-background.show {
		display: block;
	}
	.drawer {
		width: 95vw;
		height: 100vh;
		background-color: white;
		position: fixed;
		top: 0;
		right: 1vw;
		padding: 15px;
		p {
			text-align: start;
		}
		.cart-total {
			margin-top: 42px;
		}

		img {
			background: none;
			width: 70px;
		}
	}
	.cart-total {
		button {
			padding: 10px;
			cursor: pointer;
			float: left;
			background-color: #3486e6;
			border: none;
			color: white;
			text-align: center;
		}
	}
	@media (min-width: 500px) {
		.drawer {
			width: 450px;
			margin-top: 45px;
			margin-right: 62px;
		}
	}
</style>
