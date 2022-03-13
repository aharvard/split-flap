<script>
	import { onMount } from 'svelte';
	import * as SC from 'svelte-cubed';
	import * as THREE from 'three';
	import { SVGLoader } from 'three/examples/jsm/loaders/SVGLoader';
	import logo from '$lib/logo.svg?raw';

	const svgLogo = new SVGLoader().parse(logo);

	let y = 0;
	let x = Math.PI;
	let z = 0;
</script>

<SC.Canvas alpha>
	<SC.Group scale={0.05} rotation={[x, y, z]}>
		{#each svgLogo.paths as logoPath}
			<SC.Mesh
				geometry={new THREE.ExtrudeGeometry(logoPath.toShapes(false), {
					depth: 40
				})}
			/>
		{/each}
	</SC.Group>
	<SC.PerspectiveCamera position={[10, 0, 100]} />
	<SC.OrbitControls />
</SC.Canvas>

<div class="controls">
	<input type="range" bind:value={x} min={0} max={5} step={0.01} />{x}
</div>

<style>
	.controls {
		position: absolute;
		top: 0;
		left: 0;
		z-index: 10;
	}
</style>
