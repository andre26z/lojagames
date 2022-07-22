<template>
	<div class="drawer" :class="{ show: active.product_drawer }">
		<div class="cart-total" v-if="product_total">
			<p>
				<strong> Total: R$ {{ cart_total.toFixed(2) }} </strong>
			</p>
		</div>

		<cart-item-card v-for="item in items" :key="item.id" :item="item">
		</cart-item-card>
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
			return {};
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

		img {
			background: none;
			width: 70px;
		}
	}

	.button-container {
		button {
			width: 50px;
			height: 20px;
			border: none;
			padding: 10px;
			border-radius: 5px;
			margin: 0 5px 50px 5px;
			cursor: pointer;
		}
		button.remove {
		}
		button.add {
		}
	}

	@media (min-width: 500px) {
		.drawer {
			width: 450px;
			margin-top: 45px;
			margin-right: 70px;
		}
	}
</style>
