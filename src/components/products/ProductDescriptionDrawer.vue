<template>
	<div class="drawer" :class="{ show: active.product_drawer }">
		<div v-if="product" class="product-details">
			<div class="product-image">
				<img :src="product.image" />
			</div>
			<div class="text-center">
				{{ product.name }} <br />
				R${{ product.price.toFixed(2) }}
				<div class="cart-total" v-if="product_total">
					<p>{{ product_total }}</p>
					<button class="remove" @click.prevent="removeFromCart()">X</button>
				</div>
			</div>
			<!-- <p class="description">{{ product.description }}</p> -->

			<div class="button-container">
				<br />
				<button class="add" @click.prevent="addToCart()">
					Adicionar ao carrinho
				</button>
			</div>
			<div class="product-details"></div>
			<div class="cart-item-card">
				<p>Subtotal: R$ {{ cart_total.toFixed(2) }}</p>
				<p>Frete: R$ {{ frete }}</p>
				<p>Valor Total: R$ {{ cart_total.toFixed(2) }}</p>

				<button class="view-product-button">Finalizar Compra</button>
			</div>
		</div>
	</div>
</template>

<script>
	import CartSummaryPaymentCard from "../cart/CartSummaryPaymentCard.vue";

	export default {
		components: {
			CartSummaryPaymentCard,
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
			frete() {
				return this.$store.state.cart.frete;
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
			frete() {
				return this.$store.getters.frete;
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
		right: -105vw;
		padding: 15px;
		transition: right 0.5s;

		&.show {
			right: 0;
		}

		img {
			background: none;
			width: 70px;
		}
	}
	.drawer-close {
		font-size: 1.5rem;
		padding: 5px;
		border-radius: 5px;
		right: 10px;
		border: 2px solid gray;
		color: gray;
		width: 15px;
		float: right;
		cursor: pointer;
		&:hover {
			background-color: lightgray;
		}
	}

	.product-details {
		display: flex;
		justify-content: center;
		flex-direction: column;
		p.description {
			padding: 20px;
			line-height: 1.5rem;
		}
		.button-container {
			button {
				width: 150px;
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
	}

	@media (min-width: 500px) {
		.drawer {
			width: 450px;
			margin-top: 45px;
			margin-right: 70px;
		}
	}
</style>
