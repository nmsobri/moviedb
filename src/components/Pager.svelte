<script>
	export let page;
	export let total_pages;
	export let goto_page;
	import { goto } from '$app/navigation';

	function handleNavigation() {
		setTimeout(() => {
			if (page < 1) {
				page = 1;
			}

			if (page > total_pages) {
				page = total_pages;
			}

			goto(`${goto_page}${page}`);
		}, 500);
	}
</script>

<div id="pager">
	<input type="number" bind:value={page} on:change={handleNavigation} />
	<span>{page} / {total_pages}</span>
</div>

<style>
	#pager {
		width: 25%;
	}

	input {
		width: 60%;
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

	#pager-index {
		color: red;
	}
</style>
