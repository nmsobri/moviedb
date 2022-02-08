<script>
	export let movies;
	import { fade } from 'svelte/transition';
</script>

<div id="movies" transition:fade>
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
	{/each}
</div>

<style>
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
</style>
