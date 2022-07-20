<template>
	<div class="card">
		<div class="image">
			<img :src="product.image" alt="" />
		</div>
		<h3>
			{{ product.name }}
		</h3>
		<h5 class="price">Preço: R${{ product.price.toFixed(2) }}</h5>
		<!-- <p class="description">Descrição: {{ description }}</p> -->
		<p class="text-muted">{{ product.category }}</p>
		<button
			class="view-product-button"
			@click.prevent="$emit('view-product', product)"
		>
			Adicionar
		</button>
	</div>
</template>

<script>
	export default {
		props: ["product"],
		computed: {
			description() {
				return this.product.description.substring(0, 150);
			},
		},
	};
</script>

<style lang="scss">
	.card {
		color: #746a6a;
		width: 80%;
		margin: 10%;
		padding: 10px;
		background-color: rgb(255, 255, 255);
		h5.price {
			color: #3486e6;
		}
		p.description {
			font-size: 0.85rem;
		}
		p.text-muted {
			color: rgb(255, 255, 255);
		}
		h3 {
			font-weight: 100;
		}
	}
	button.view-product-button {
		padding: 10px;
		color: #3486e6;
		border: none;
		font-weight: bold;

		cursor: pointer;
	}
	@media (min-width: 500px) {
		.card {
			width: 350px;
			margin: 10px;
		}
	}
</style>
