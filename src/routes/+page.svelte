<script lang="ts">
	import { onMount} from "svelte";
	import Card from "./Card.svelte";
	import { searchStore } from "./store";

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

	const API_KEY = import.meta.env.VITE_API_KEY;

	let currentPage: number = 1;
	let totalPages: number = 0;

	const IMGPATH = 'https://image.tmdb.org/t/p/w500'

	let movies: moviesObject[] = [];

	function constructUrl(searchTerm: string = ''): string {
		if (searchTerm) {
			return `https://api.themoviedb.org/3/search/movie?api_key=${API_KEY}&language=en-US&include_adult=false&query=${searchTerm}&page=${currentPage}`;
		}
		return `https://api.themoviedb.org/3/movie/popular?api_key=${API_KEY}&language=en-US&page=${currentPage}`;
	}

	async function fetchData(url: string): Promise<void> {
		const response = await fetch(url);
		const data = await response.json();
		movies = data.results;
		totalPages = data.total_pages;
	}

	function handlePageChange(nextORPrev: "prev" | "next"): void {
		switch (nextORPrev) {
			case "prev":
				if (currentPage > 1) {
					currentPage = currentPage - 1;
				}	
				break;
			case "next":
				if (currentPage < totalPages) {
					currentPage = currentPage + 1;
				}
				break;
			default:
				break;
		}
		fetchData(constructUrl()); // fetch new page data here
	}

	onMount(() => fetchData(constructUrl()));
	$: {
		fetchData(constructUrl($searchStore));
	}
</script>

<svelte:head>
	<title>Movies App in Sveltekit</title>
	<meta name="description" content="a movies app in svltekit" />
</svelte:head>

<section class="page">
	<p>{currentPage} of {totalPages}</p>
	<div>
		<button on:click={() => handlePageChange("prev")}>{"<"}</button>
		<button on:click={() => handlePageChange("next")}>{">"}</button>
	</div>
</section>
<section>
	<ul>
		{ #each movies as movie (movie.id) }
			<Card src={IMGPATH + movie.poster_path} alt={movie.title} title={movie.title} desc={movie.overview} />
		{/each}
	</ul>
</section>
<section class="page">
	<p>{currentPage} of {totalPages}</p>
	<div>
		<button on:click={() => handlePageChange("prev")}>{"<"}</button>
		<button on:click={() => handlePageChange("next")}>{">"}</button>
	</div>
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
	.page {
		margin-block: 20px;
	}
	.page div {
		display: flex;
		max-width: 500px;
	}
</style>
