<template>
	<div class="home">
		<h1>GAMES</h1>
		<p>
			<select
				v-model="selectedValue"
				name=""
				id=""
			>
				<option value="1">Melhores Avaliados</option>
				<option value="2">Preço &#x2191 </option>
				<option value="3">Preço &#x2193 </option>
				<option value="4">Ordem alfabética</option>
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

	export default {
		name: "HomeVue",
		components: {
			ProductSummaryCard,
			ProductDescriptionDrawer,
		},

		data() {
			return {
				items: items,
				product: null,
				active: {
					product_drawer: true,
				},
				selectedValue: 1,
			};
		},
		methods: {
			viewProduct(product) {
				this.product = product;
				this.active.product_drawer = true;
			},
		},
		computed: {
			items() {
				if (this.selectedValue == 1) {
					return this.items.sort((a, b) => b.score - a.score);
				} else if (this.selectedValue == 2) {
					return this.items.sort((a, b) => b.price - a.price);
				} else if (this.selectedValue == 3) {
					return this.items.sort((a, b) => a.price - b.price);
				} else {
					return this.items.sort((a, b) => a.name.localeCompare(b.name));
				}
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
			transform: translate(261px, -45px);
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
	.asc:after {
		content: "\25B2";
	}

	.desc:after {
		content: "\25BC";
	}
</style>
