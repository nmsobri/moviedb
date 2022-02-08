<script>
	import { fly, fade } from 'svelte/transition';
	import Pager from '../components/Pager.svelte';
	import { goto } from '$app/navigation';

	let search_input = '';
	let show_button = false;
	let show_label = true;
	export let page = 1;
	export let total_pages = 1;

	$: show_button = search_input.length >= 3 ? true : false;

	function showLabel() {
		show_label = search_input.length >= 3 ? false : true;
		if (search_input.length >= 3) {
			show_label = false;
		} else {
			show_label = true;
			search_input = '';
		}
	}

	function searchMovie() {
		let path = `/search/${search_input}`;
		goto(path);
	}
</script>

<div id="top-bar">
	<form class="search" on:submit|preventDefault={searchMovie}>
		{#if show_label}
			<label for="search" transition:fly={{ x: -10, y: 0 }}>Search Movie</label>
		{/if}

		<input
			class:selected={!show_label}
			id="search"
			type="text"
			bind:value={search_input}
			on:focus={() => (show_label = false)}
			on:blur={showLabel}
		/>

		{#if show_button}
			<button class:hide={!show_button} transition:fade>Search</button>
		{/if}
	</form>

	<Pager page={page} total_pages={total_pages} goto_page={`/page/`} />
</div>

<style>
	#top-bar {
		display: flex;
		justify-content: space-between;
		margin:1rem;
	}

	.hide {
		visibility: hidden;
	}

	.search {
		position: relative;
		width: 30%;
		flex-wrap: wrap;
		justify-content: flex-end;
	}

	label {
		position: absolute;
		font-size: 0.8rem;
		top: 50%;
		left: 0;
		transform: translate(0, -50%);
		pointer-events: none;
		color: white;
		padding: 0 1rem;
	}

	input {
		width: 100%;
		border: none;
		font-size: 1rem;
		font-family: 'Poppins', sans-serif;
		outline: none;
		color: white;
		padding: 0.5rem 0.1rem;
		transition: background 0.75s ease-out;
		font-weight: bold;
		background: rgb(63, 63, 63);
		border-radius: 10px;
		padding: 1rem;
	}

	input.selected {
		background: rgb(56, 56, 56);
	}

	button {
		font-size: 0.7rem;
		padding: 0rem 1rem;
		background: rgb(96, 110, 201);
		color: white;
		font-weight: bold;
		border: none;
		position: absolute;
		bottom: 50%;
		right: 0;
		transform: translate(0, 50%);
		height: 100%;
		border-top-right-radius: 10px;
		border-bottom-right-radius: 10px;
		cursor: pointer;
	}
</style>
