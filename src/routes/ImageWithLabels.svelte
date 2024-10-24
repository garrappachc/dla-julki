<script module lang="ts">
	import type { Label } from './labels';

	export const labels: Label[] = $state([
		{
			id: 0,
			position: { x: 10, y: 10 },
			text: 'Label 1',
			style: 'color: #000000;\nfont-size: 14px;\nmax-width: 100px;'
		}
	]);
</script>

<script lang="ts">
	import html2canvas from 'html2canvas';

	interface Props {
		src: string;
	}

	let { src }: Props = $props();
	let target: HTMLDivElement;

	function download() {
		html2canvas(target).then((canvas) => {
			const link = document.createElement('a');
			link.download = 'image.png';
			link.href = canvas.toDataURL();
			link.click();
		});
	}
</script>

<div class="flex items-center gap-8">
	<div bind:this={target} class="relative w-[1080px] h-[1080px]">
		<img alt="template" {src} />

		{#each labels as l}
			<span
				class="absolute"
				style="
        top: {l.position.y}px;
        left: {l.position.x}px;
        {l.style}
        ">{l.text}</span
			>
		{/each}
	</div>

	<button onclick={download}>Download</button>
</div>
