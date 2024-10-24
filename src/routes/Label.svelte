<script lang="ts">
	import { labels } from './ImageWithLabels.svelte';

	let { id, maxX, maxY }: { id: number; maxX: number; maxY: number } = $props();

	function onTextChange(event: Event) {
		labels[id].text = (event.target as HTMLInputElement)!.value;
	}

	function onPositionXChange(event: Event) {
		labels[id].position.x = Number((event.target as HTMLInputElement)!.value);
	}

	function onPositionYChange(event: Event) {
		labels[id].position.y = Number((event.target as HTMLInputElement)!.value);
	}

	function onStyleChange(event: Event) {
		labels[id].style = (event.target as HTMLInputElement)!.value;
	}

	function remove() {
		labels.splice(id, 1);
	}
</script>

<div class="flex flex-row gap-2 items-start">
	<span>Text:</span>
	<input
		type="text"
		class="bg-gray-50 border border-gray-300 text-gray-900 text-sm"
		value={labels[id].text}
		onchange={onTextChange}
	/>
	<span>x:</span>
	<input
		type="number"
		min="0"
		max={maxX}
		step="1"
		class="bg-gray-50 border border-gray-300 text-gray-900 text-sm"
		value={labels[id].position.x}
		onchange={onPositionXChange}
	/>
	<span>y:</span>
	<input
		type="number"
		min="0"
		max={maxY}
		step="1"
		class="bg-gray-50 border border-gray-300 text-gray-900 text-sm"
		value={labels[id].position.y}
		onchange={onPositionYChange}
	/>
	<span>style:</span>
	<textarea
		class="bg-gray-50 border border-gray-300 text-gray-900 text-sm"
		onchange={onStyleChange}
		rows="6">{labels[id].style}</textarea
	>
	<button onclick={remove}>remove</button>
</div>
