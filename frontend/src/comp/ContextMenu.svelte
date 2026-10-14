<script module lang="ts">
	export type Data = {
		text: string;
		f: () => void;
	};

	export const DEFAULT_PLACEMENT = { left: -200, top: -200 };
</script>

<script lang="ts">
	import Borderd from './Borderd.svelte';
	import Button from './Button.svelte';

	let {
		left = $bindable(DEFAULT_PLACEMENT.left),
		top = $bindable(DEFAULT_PLACEMENT.top),
		show = $bindable(false),
		data = $bindable([] as Data[])
	} = $props();
</script>

<Borderd
	className={'z-[9999] absolute bg-black'}
	style="left: {left}px;top: {top}px;opacity: {Number(show)}"
>
	<div
		aria-roledescription=""
		id="contextmenu"
		class="w-32"
		onmousedown={(e) => e.stopPropagation()}
	>
		{#each data as entry}
			<Button
				type="primary"
				onclick={() => {
					entry.f();
                    show = false;
				}}>{entry.text}</Button
			>
		{/each}
	</div>
</Borderd>
