<script context="module">
	export async function load({ fetch, params }) {
		const res = await fetch(
			`https://api.themoviedb.org/3/movie/${params.id}?api_key=11254cd956c752d59d0519874dbafd7d&language=en-US`
		);

		const json = await res.json();

		return {
			props: {
				movie: json
			}
		};
	}
</script>

<script>
	export let movie;
	import { fade } from 'svelte/transition';
</script>

<svelte:head>
	<title>{movie.original_title}</title>
</svelte:head>

<div class="movie" transition:fade>
	<div class="img">
		<img src={`https://image.tmdb.org/t/p/original${movie.backdrop_path}`} alt={movie.title} />
	</div>

	<div class="text">
		<h1>{movie.title}</h1>
		<p class="overview">{movie.overview}</p>
		<p>
			<span>Release date:</span>
			{movie.release_date} <br />
			<span>Budget:</span>
			{movie.budget} <br />
			<span>Rating:</span>
			{movie.vote_average} <br />
			<span>Runtime:</span>
			{movie.runtime}mins
		</p>
	</div>
</div>

<style>
	h1 {
		margin: 1rem 0rem 1rem;
	}

	p {
		margin: 1rem 0rem;
	}

	.img {
		width: 100%;
	}

	img {
		width: 100%;
		border-radius: 1rem;
	}

	.movie {
		margin: 2rem 20%;
	}

	span {
		font-weight: bold;
	}

	.text {
		padding: 0.5rem;
	}
</style>
