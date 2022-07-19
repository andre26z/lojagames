<template>
	<div class="home">
		<h1>GAMES</h1>

		<ProductDescriptionDrawer
			:product="product"
			:active="active"
			v-on:closeProductDrawer="closeProductDrawer()"
		/>
		<div class="product-cards-container">
			<ProductSummaryCard
				v-for="(item, i) in items"
				:key="i"
				:product="item"
				v-on:view-product="viewProduct($event)"
			/>
		</div>
		<cart-summary-payment-card></cart-summary-payment-card>
	</div>
</template>

<script>
	import items from "../data/items.js";
	import ProductSummaryCard from "../components/products/ProductSummaryCard.vue";
	import ProductDescriptionDrawer from "../components/products/ProductDescriptionDrawer.vue";
	import CartSummaryPaymentCard from "../components/cart/CartSummaryPaymentCard.vue";

	export default {
		name: "HomeVue",
		components: {
			ProductSummaryCard,
			ProductDescriptionDrawer,
			CartSummaryPaymentCard,
		},
		data() {
			return {
				items: items,
				product: null,
				active: {
					product_drawer: false,
				},
			};
		},
		methods: {
			viewProduct(product) {
				this.product = product;
				this.active.product_drawer = true;
			},
			closeProductDrawer() {
				this.active.product_drawer = false;
			},
		},
	};
</script>

<style lang="scss">
	* {
		font-family: sans-serif;
		a {
			color: rgb(0, 0, 0);
		}
	}

	.home {
		background-color: rgba(254, 252, 255, 0.815);
		h1 {
			color: rgb(0, 0, 0);
			margin-right: 90%;
			display: inline-flex;
		}
		span {
			display: inline-flex;
		}
	}
	.product-cards-container {
		display: inline-flex;
		flex-wrap: wrap;
		justify-content: center;
		width: 70%;
		margin-left: -400px;
		// background-color: rgb(56, 44, 68);
	}
	img {
		width: 70%;
		background-color: rgb(221, 221, 221);
		padding: 33px;
	}
</style>
