<script>
	import Counter from './Counter.svelte';
	import welcome from '$lib/images/svelte-welcome.webp';
	import welcome_fallback from '$lib/images/svelte-welcome.png';
	let api_key = import.meta.env.VITE_API_KEY;
	console.log(api_key);
</script>

<svelte:head>
	<title>Movies App in Sveltekit</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<header></header>
	<main>

	</main>
	<footer></footer>
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		width: 100%;
	}

	.welcome {
		display: block;
		position: relative;
		width: 100%;
		height: 0;
		padding: 0 0 calc(100% * 495 / 2048) 0;
	}

	.welcome img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}
</style>
