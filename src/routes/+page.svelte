<script lang="ts">
	import { onMount } from "svelte";
	import Card from "./Card.svelte";

	const API_KEY = import.meta.env.VITE_API_KEY;
	const BASEURL = `https://api.themoviedb.org/3/movie/popular?api_key=${API_KEY}&language=en-US&page=1`
	const SEARCHURL = `https://api.themoviedb.org/3/search/movie?api_key=${API_KEY}&language=en-US&include_adult=false&query=`
	const IMGPATH = 'https://image.tmdb.org/t/p/w500'

	type moviesObject = {
		adult: boolean,
		backdrop_path: string,
		genre_ids: number[],
		id: number,
		original_language: string,
		original_title: string,
		overview: string,
		popularity: number,
		poster_path: string,
		release_date: string,
		title: string,
		video: boolean,
		vote_average: number,
		vote_count: number
	}

	let movies: moviesObject[] = [];
	$: console.log(movies);

	async function fetchData(): Promise<void> {
		const response = await fetch(BASEURL);
		const data = await response.json();
		movies = data.results;
	}

	onMount(fetchData)
</script>

<svelte:head>
	<title>Movies App in Sveltekit</title>
	<meta name="description" content="a movies app in svltekit" />
</svelte:head>

<section>
	<ul>
		{ #each movies as movie (movie.id) }
			<Card src={IMGPATH + movie.poster_path} alt={movie.title} title={movie.title} desc={movie.overview} />
		{/each}
	</ul>
</section>

<style>
	ul {
		display: flex;
		flex-wrap: wrap;
		justify-content: flex-start;
		align-items: center;
		padding: 0;
		margin: 0;
		list-style: none;
		gap: 20px;
	}
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}
</style>
