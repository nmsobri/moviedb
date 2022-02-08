<script>
	import app from '../app.css';
</script>

<svelte:head>
	<meta charset="utf-8" />
	<meta name="robots" content="index,follow" />
	<meta name="viewport" content="width=device-width, initial-scale=1" />
	<meta name="description" content="Learn Html & Css From Scratch" />
	<link rel="icon" href="favicon.ico" />
	<title>Movie Database</title>
</svelte:head>

<p id="title">
	<a href="/">Movie Db</a>
</p>

<slot />

<style>
	#title {
		margin: 1rem auto;
		text-align: center;
		font-weight: bold;
		font-size: 1.5rem;
		text-shadow: 1px 1px 3px gray;
	}

	#title > a {
		color:black;
		text-decoration: none;
	}
</style>
