<template>
	<div class="home">
		<h1>GAMES</h1>
		<p>
			<select name="" id="">
				<option value="">Mais jogados</option>
			</select>
		</p>

		<ProductDescriptionDrawer :product="product" :active="active" />

		<div class="product-cards-container">
			<ProductSummaryCard
				v-for="(item, i) in items"
				:key="i"
				:product="item"
				v-on:view-product="viewProduct($event)"
			/>
		</div>
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
					product_drawer: true,
				},
			};
		},
		methods: {
			viewProduct(product) {
				this.product = product;
				this.active.product_drawer = true;
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
			margin-right: 78%;
		}
		select {
			color: black;
			display: inline-flex;
			transform: translate(290px, -45px);
		}
	}
	.product-cards-container {
		display: inline-flex;
		flex-wrap: wrap;
		justify-content: center;
		width: 70%;
		margin-left: -400px;
		margin-top: -48px;
		// background-color: rgb(56, 44, 68);
	}
	img {
		width: 180px;
		background-color: #eeeeee;
		padding: 33px;
	}
</style>
