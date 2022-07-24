<template>
	<div class="home">
		<div class="container">
			<h1>GAMES</h1>

			<div class="seletor">
				<select v-model="selectedValue" name="" id="">
					<option value="1">Mais populares</option>
					<option value="2">Preço &#x2191;</option>
					<option value="3">Preço &#x2193;</option>
					<option value="4">Ordem alfabética</option>
				</select>
			</div>
		</div>

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
		.container {
			display: flex;
			width: 1223px;

			h1 {
				color: rgb(0, 0, 0);
				display: inline-flex;
				padding-left: 20px;
				padding-right: 30px;
			}
			select {
				color: #423b3b;
				display: inline-flex;
				height: 20px;
				margin-top: 26px;
				align-self: center;
				border: #e1e1e1 solid 1px;
				border-radius: 4px;
				height: 32px;
				cursor: pointer;
			}
		}
	}
	.product-cards-container {
		display: inline-flex;
		flex-wrap: wrap;
		justify-content: center;
		width: 70%;
		margin-left: -400px;
		margin-top: -27px;
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
	@media (min-width: 1441px) {
		.container {
			justify-content: space-between;
		}
		select {
			padding-right: 124px;
		}
	}
	@media (max-width: 426px) {
		.product-cards-container {
			width: 100%;
			margin-left: 0;
			margin-top: -27px;
		}
	}
</style>
