<script context="module">
	export async function load({ fetch, params }) {

		const res = await fetch(
			`https://api.themoviedb.org/3/movie/popular?api_key=11254cd956c752d59d0519874dbafd7d&language=en-US&page=${params.page}`
		);

		const json = await res.json();

		return {
			props: {
				movies: json.results,
				total_pages: json.total_pages,
				page: params.page
			}
		};
	}
</script>

<script>
	export let page;
	export let movies;
	export let total_pages;
	import Movies from '../../components/Movies.svelte';
</script>

<main>
	<Movies movies={movies} page={page} total_pages={total_pages} />
</main>
