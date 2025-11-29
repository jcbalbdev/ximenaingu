<script lang="ts">
	import Header from '$lib/components/Header.svelte';
	import Footer from '$lib/components/Footer.svelte';
	import '../app.css';

	/* con esto se hereda el contenido de las diferentes páginas */
	let { children } = $props();
</script>

<div class="app">
	<Header />

	<main>
		<!-- esto funciona como un slot en astro -->
		{@render children()}
	</main>
<Footer />

</div>

<style>
	.app {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
		background: linear-gradient(
  180deg,
  #2d3a2d 0%,
  #5c5442 50%,
  #8b7355 100%
);
background-attachment: fixed;
min-height: 100vh;
	}

	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		padding: 1rem;
		width: 100%;
		max-width: 90rem;
		margin: 0 auto;
		box-sizing: border-box;
		
	}


</style>
