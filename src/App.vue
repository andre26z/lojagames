<template>
	<div>
		<nav>
			<router-link :class="{ active: $route.name === 'Home' }" to="/"
				></router-link
			>
			<router-link
				:class="{ active: $route.name === 'CartShopping' }"
				to="/cart"
				>
			</router-link>
		</nav>
		
		<router-view />
	</div>
</template>

<style lang="scss">
	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #2c3e50;
	}

	html,
	body {
		margin: 0;
		padding: 0;
		overflow-x: hidden;
	}



	#nav {
		padding: 10px;
		width: 100%;
		height: 30px;
		background-color: white;
		line-height: 30px;
	}
	a {
		font-weight: bold;
		color: rgb(0, 0, 0);
		text-decoration: none;
		margin: 0 5px 0 5px;
		font-size: 1.25rem;

		&.active {
			color: #000000;
		}
	}
	.text-center {
		text-align: center;
	}
</style>
