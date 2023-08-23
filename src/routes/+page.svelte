<script lang="ts">
	import { onMount } from 'svelte'

	let canvasElem: HTMLCanvasElement
	let pixelDataString: string

	const draw = () => {
		if (!canvasElem) {
			return
		}

		const context = canvasElem.getContext('2d')
		if (!context) {
			return
		}

		context.font = '48px'
		context.fillText('How quickly daft jumping zebras vex', 10, 50)
	}

	const getPixelData = () => {
		if (!canvasElem) {
			return
		}

		const pixelDataBase64Encoded = canvasElem.toDataURL()
		pixelDataString = pixelDataBase64Encoded
	}

	onMount(draw)
</script>

<main class="content-wrapper">
	<div>This is for examining the "Canvas Fingerprinting" method.</div>
	<section class="content-section">
		<canvas bind:this={canvasElem} class="canvas" />
		<button type="button" class="get-pixel-data-button" on:click={getPixelData}>GET PIXEL DATA</button>
		<textarea bind:value={pixelDataString} readonly class="textarea" />
	</section>
</main>

<style>
	.content-wrapper {
		display: flex;
		flex-direction: column;
		align-items: center;
	}
	.content-section {
		display: flex;
		flex-direction: column;
	}

	.canvas {
		border: 1px solid bisque;
		margin-top: 24px;
	}

	.textarea {
		resize: none;
		height: 500px;
	}
	.get-pixel-data-button {
		background-color: bisque;
		border: none;
		border-radius: 8px;
		padding: 6px 8px;
		margin: 24px 0;
		cursor: pointer;

		&:hover {
			background-color: antiquewhite;
		}
	}
</style>
