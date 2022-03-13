<script>
	import { fly } from 'svelte/transition';
	import Star from '$lib/Star.svelte';

	let isStar = false;

	function hitButton() {
		isStar = true;
		setTimeout(() => {
			isStar = false;
		}, 40);
	}
</script>

<header>
	<h1>Star World</h1>
</header>

<div style:position="relative">
	{#if isStar}
		<div class="star" out:fly={{ opacity: 0, y: -100, duration: 3000 }}>
			<Star />
		</div>
	{/if}
	<button on:click={hitButton}>Level Up</button>
</div>

<style>
	header {
		display: flex;
		font-family: Arial, Helvetica, sans-serif;
		margin-bottom: 60px;
	}

	.star {
		position: absolute;
		top: -30px;
		z-index: -1;
	}
</style>
