<script>
	import Movie from '../components/Movie.svelte';
	import TopBar from './TopBar.svelte';
	export let movies;
	export let page = 1;
	export let total_pages = 1;
</script>

<svelte:head>
	<title>Movie Database</title>
</svelte:head>

<TopBar page={page} total_pages={total_pages} />

<Movie movies={movies} />