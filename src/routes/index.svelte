<script context="module">
	let page = 1;
	export async function load({ fetch, params }) {
		const res = await fetch(
			`https://api.themoviedb.org/3/movie/popular?api_key=11254cd956c752d59d0519874dbafd7d&language=en-US&page=${page}`
		);

		const json = await res.json();

		return {
			props: { movies: json.results, page: page, total_pages: json.total_pages }
		};
	}
</script>

<script>
	export let movies;
	export let total_pages;
	import Movies from '../components/Movies.svelte';
</script>

<main>
	<Movies movies={movies} page={1} total_pages={total_pages} />
</main>
