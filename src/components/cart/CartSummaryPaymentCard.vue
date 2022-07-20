 <template>
	<div class="cart-item-card">
		<p>Subtotal: R$ {{ cart_total.toFixed(2) }} <button></button></p>
		<p>Frete: R$</p>
		<p>Valor Total: R$ {{ cart_total.toFixed(2) }}</p>

		<button class="view-product-button">Finalizar Compra</button>
	</div>
</template>

<script>
	export default {
		props: ["products"],
		computed: {
			cart_total() {
				return this.$store.getters.cartItems.reduce(
					(a, b) => a + b.price * b.quantity,
					0
				);
			},
		},
	};
</script>

<style lang="scss" scoped>
	.cart-item-card {
		position: absolute;
		display: inline-flex;
		flex-direction: column;
		width: 262px;
		height: 325px;
		justify-content: center;
		align-items: center;
		border: black solid 1px;
		float: right;
	}
	img {
		width: 30%;
	}
</style> 
