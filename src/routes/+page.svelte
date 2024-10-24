<script lang="ts">
	import Label from './Label.svelte';
	import ImageWithLabels, { labels } from './ImageWithLabels.svelte';
	import html2canvas from 'html2canvas';

	let imgUpload: HTMLInputElement;
	let imgTemplate: HTMLImageElement;
	let target: HTMLDivElement;

	let maxX = $state(1080);
	let maxY = $state(1080);
	let posX = $state(0);
	let posY = $state(0);
	let src = $state('https://placehold.co/1080x1080');

	function onchange(event: Event) {
		const [file] = imgUpload.files ?? [];
		if (file) {
			src = URL.createObjectURL(file);
		}
	}

	function onload() {
		maxX = imgTemplate.width;
		maxY = imgTemplate.height;
	}

	function download() {
		html2canvas(target).then((canvas) => {
			const link = document.createElement('a');
			link.download = 'image.png';
			link.href = canvas.toDataURL();
			link.click();
		});
	}
</script>

<div class="flex flex-row gap-2">
	<span>Pick image template:</span>
	<input type="file" accept="image/*" {onchange} {onload} bind:this={imgUpload} />
</div>

{#each labels as l}
	<Label id={l.id} {maxX} {maxY} />
{/each}

<div>
	<button
		onclick={() =>
			labels.push({
				id: labels.length,
				position: { x: posX, y: posY },
				text: 'Label ' + (labels.length + 1),
				style: 'color: #000000; font-size: 14px; max-width: 100px;'
			})}>Add label</button
	>
</div>

<ImageWithLabels {src} />
