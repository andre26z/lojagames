<template>
	<div class="drawer" :class="{ show: active.product_drawer }">
		<cart-item-card v-for="item in items" :key="item.id" :item="item">
		</cart-item-card>

		<div class="cart-total" v-if="cart_total > 0">
			<p>Frete: {{ frete.toFixed(2) }}</p>
			<p>
				<strong> Total: R$ {{ cart_total.toFixed(2) }} </strong>
			</p>
			<button class="finalizarcompra">FINALIZAR COMPRA</button>
		</div>
		<div class="carrinhovazio" v-else>
			<h1>Carrinho</h1>
			<br />
			<img src="../../assets/carrinhovazio.png" alt="" />
			<h6>Até o momento o seu carrinho está vazio</h6>
		</div>
	</div>
</template>

<script>
	import CartItemCard from "../cart/CartItemCard.vue";
	export default {
		components: {
			CartItemCard,
		},

		props: ["product", "active"],

		data() {
			return {
				frete: 0,
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

		&.show {
			display: block;
		}
	}
	.drawer-background.show {
		display: block;
	}
	.drawer {
		display: flex;
		flex-direction: column;
		width: 450px;
		margin-right: 62px;
		height: 100vh;
		background-color: white;
		position: fixed;
		top: 0;
		right: 1vw;
		padding: 15px;
		overflow: auto;
		p {
			text-align: start;
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
	@media (max-width: 768px) {
		.drawer {
			width: 54%;
			margin-right: 0;
		}
	}
	@media (max-width: 426px) {
		.drawer {
			width: 127%;
			margin-right: 0;
			position: relative;
			height: fit-content;
		}
	}
	@media (max-width: 326px) {
		.drawer {
			width: 100%;
			margin-right: 0;
			position: relative;
			height: fit-content;
			display: flex;
		}
	}
</style>
