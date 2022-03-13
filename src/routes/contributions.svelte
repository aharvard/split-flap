<script>
	import * as THREE from 'three';
	import * as SC from 'svelte-cubed';
	import { spring } from 'svelte/motion';

	let rows = 50;
	let depth = 50;
	let hue = Math.round(Math.random() * 360);

	let contributions = spring(getContributions());

	function refresh() {
		$contributions = getContributions();
		hue = Math.round(Math.random() * 360);
	}

	function getContributions() {
		return new Array(rows * depth).fill(0).map((value) => {
			return Math.round(Math.random() * 10);
		});
	}
</script>

<div class="controls">
	<button on:click={refresh}>Refresh</button>
</div>

<SC.Canvas antialias alpha>
	{#each $contributions as contribution, index}
		<SC.Mesh
			scale={[1, contribution, 1]}
			geometry={new THREE.BoxGeometry()}
			material={new THREE.MeshStandardMaterial({
				color: `hsl(${hue}, 50%, ${contribution * 10}%)`
			})}
			position={[Math.floor(index / rows), contribution / 2, index % rows]}
		/>
	{/each}
	<SC.PerspectiveCamera position={[15, 15, 15]} />
	<SC.OrbitControls />
	<SC.AmbientLight intensity={0.5} />
	<SC.DirectionalLight intensity={1} position={[3, 5, -4]} />
</SC.Canvas>

<style>
	.controls {
		position: absolute;
		z-index: 10;
	}
</style>
