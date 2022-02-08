<script context="module">
	export async function load({ fetch, params }) {
		let page = params.page;

		const res = await fetch(
			`https://api.themoviedb.org/3/search/movie?api_key=11254cd956c752d59d0519874dbafd7d&language=en-US&page=${page}&include_adult=false&query=${params.name}`
		);

		const json = await res.json();

		return {
			props: {
				movies: json.results,
				page: page,
				total_pages: json.total_pages,
				search_term: params.name
			}
		};
	}
</script>

<script>
	export let movies;
	export let page = 1;
	export let total_pages = 1;
	export let search_term;
	import Pager from '../../../components/Pager.svelte';
</script>

<svelte:head>
	<title>Movie Database [ {search_term} ]</title>
</svelte:head>

<div id="top-bar">
	<Pager page={page} total_pages={total_pages} goto_page={`/search/${search_term}/`} />
</div>

<div id="movies">
	{#each movies as movie}
		<div class="movie">
			<a sveltekit:prefetch href={`/movie/${movie.id}`}>
				<img src={`https://image.tmdb.org/t/p/w300/${movie.poster_path}`} alt={movie.title} />
			</a>
			<div class="description">
				<h2>
					{movie.title}
				</h2>

				<p>
					{movie.release_date}
				</p>
			</div>
		</div>
	{:else}
		<div id="not-found">
			<div>No movies found</div>
		</div>
	{/each}
</div>

<style>
	#top-bar {
		padding: 1rem;
		display: flex;
		justify-content: flex-end;
	}

	#movies {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
		grid-column-gap: 1rem;
		grid-row-gap: 2rem;
		margin: 1rem;
	}

	img {
		width: 100%;
		object-fit: cover;
		border-radius: 1rem;
		margin-bottom: 1rem;
	}

	h2 {
		font-size: 0.9rem;
	}

	.description {
		height: 5vh;
	}

	p {
		font-size: 0.7rem;
	}
	#not-found {
		display: grid;
		grid-template-columns: 1fr;
		grid-auto-rows: 300px;
		margin-top: 2rem;
	}

	#not-found > div {
		font-weight: bold;
		font-size: 1.3rem;
		padding: 2rem;
		width: 60%;
		text-align: center;
		border: 2px solid gray;
		margin: 0 auto;

		display: flex;
		justify-content: center;
		align-content: center;
		flex-direction: column;
	}
</style>
