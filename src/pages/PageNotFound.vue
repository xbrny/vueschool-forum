<template>
	<div>
		<h1>Page Not Found</h1>
		<p>Oops! Looks like the page you are trying to find cannot be found. Why dont' you
			<router-link :to="{ name: 'PageHome' }"> go back home?</router-link>
		</p>
	</div>
</template>

<script>
</script>

<style scoped>
	h1 {
		font-size: 100px;
	}
	p {
		font-size: 50px;
		font-weight: 100;
	}
	div {
		margin-top: 3em;
		text-align: center;
	}
</style>