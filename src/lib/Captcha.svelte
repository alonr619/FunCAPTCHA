<script lang="ts">
	import { gsap, Draggable } from '$lib/gsap';
	import { onMount } from 'svelte';
	import * as all from '$lib/svgs';

	function shuffle(array: any[]) {
		for (let i = array.length - 1; i > 0; i--) {
			const j = Math.floor(Math.random() * (i + 1));
			[array[i], array[j]] = [array[j], array[i]];
		}
	}

	const colors = ['#ff0', '#f0f', '#0ff', '#f00', '#0f0', '#00f'];
	const options = Object.keys(all);
	let left: string;
	let right: string;
	let positions: number[][] = [
		[900, 0],
		[900, 300],
		[900, 600],
		[300, 0],
		[300, 300],
		[300, 600]
	];
	let identifiers: string[][] = [
		['left', '0'],
		['left', '1'],
		['left', '2'],
		['right', '0'],
		['right', '1'],
		['right', '2']
	];
	let components: any[];

	let state = 0; // 0 means loading, 1 means ready, 2 means in-progress, 3 means success, 4 means failure
	let leftComplete: number[] = [0, 0, 0];
	let rightComplete: number[] = [0, 0, 0];
	$: complete =
		leftComplete.reduce((a, b) => a + b, 0) === 3 && rightComplete.reduce((a, b) => a + b, 0) === 3;

	onMount(async () => {
		shuffle(positions);
		const leftIndex = Math.floor(Math.random() * options.length);
		left = options[leftIndex];
		options.splice(leftIndex, 1);
		const rightIndex = Math.floor(Math.random() * options.length);
		right = options[rightIndex];
		components = all[left].concat(all[right]);
		state = 1;
	});

	function start() {
		Draggable.create('.icon', {
			bounds: 'svg',
			onDrag: function () {
				if (this.hitTest('#left')) {
					gsap.to(this.target, { duration: 0.6, opacity: 0, scale: 0 });
					if (this.target.classList.contains('left')) {
						let cur = this.target.id;
						leftComplete[parseInt(cur.substring(cur.length - 1))] = 1;
						if (complete) {
							state = 3;
						}
					} else {
						state = 4;
					}
				} else if (this.hitTest('#right')) {
					gsap.to(this.target, { duration: 0.6, opacity: 0, scale: 0 });
					if (this.target.classList.contains('right')) {
						let cur = this.target.id;
						rightComplete[parseInt(cur.substring(cur.length - 1))] = 1;
						if (complete) {
							state = 3;
						}
					} else {
						state = 4;
					}
				}
			}
		});
		state = 2;
	}
</script>

<svg
	version="1.1"
	id="Layer_1"
	xmlns="http://www.w3.org/2000/svg"
	xmlns:xlink="http://www.w3.org/1999/xlink"
	x="0px"
	y="0px"
	viewBox="0 0 1600 860"
	style="enable-background:new 0 0 800 430;"
	xml:space="preserve"
	preserveAspectRatio="none"
>
	{#if state === 0}
		<text fill="blue">Loading...</text>
	{:else if state === 1 || state === 2}
		{#each components as image, i}
			<svelte:component
				this={image}
				className={identifiers[i][0]}
				id={identifiers[i][0] + identifiers[i][1]}
				color={colors[Math.floor(Math.random() * colors.length)]}
				translate={positions[i]}
				scale={[Math.random() * 1.5 + 0.5, 0.8]}
			/>
		{/each}
		<rect
			width="100"
			height="860"
			style="fill:{colors[Math.floor(Math.random() * colors.length)]};"
			id="left"
		/>
		<rect
			width="100"
			height="860"
			x="1500"
			style="fill:{colors[Math.floor(Math.random() * colors.length)]};"
			id="right"
		/>
		<text
			x="10"
			height="0"
			transform="translate(0,{Math.floor(Math.random() * 400) + 50})scale({Math.random() * 4 +
				2})rotate(90 5,0)">{left}</text
		>
		<text
			x="10"
			height="0"
			transform="translate(1510,{Math.floor(Math.random() * 400) + 50})scale({Math.random() * 4 +
				2})rotate(90 5,0)">{right}</text
		>
	{:else if state === 3}
		<text fill="green" x="50" y="50" transform="scale(10)">Success!</text>
	{:else if state === 4}
		<text fill="red" x="50" y="50" transform="scale(10)">Failure</text>
	{/if}
</svg>

<button disabled={state !== 1} on:click={start}>Start</button>

<style>
	svg {
		display: block;
		position: relative;
		width: 800px;
		background: #1d1d1d;
		margin: 20px auto;
		border: 10px solid black;
	}

	button {
		font-size: 5em;
		margin-left: 45%;
	}
</style>
