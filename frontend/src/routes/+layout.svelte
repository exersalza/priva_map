<script lang="ts">
	import './layout.css';
	import favicon from '#lib/assets/favicon.svg';
	import type { LayoutProps } from './$types';
	import ContextMenu, { DEFAULT_PLACEMENT } from '../comp/ContextMenu.svelte';
	import { getContext, type Snippet } from 'svelte';

	let { children }: { children: Snippet } = $props();

	let context = $state({ ...DEFAULT_PLACEMENT, show: false });
	const registerContextMenu =
		getContext<(buttons: Array<{ text: string; f: () => void }>) => void>('registerContextMenu');
	// Define your global context menu actions here if they apply app-wide

	const contextMenu = (e: PointerEvent) => {
		e.preventDefault();
		let pad = 10;
		let cm = document.getElementById('contextmenu');
		let x = Math.min(e.x, window.innerWidth - ((cm?.clientWidth ?? 0) + pad));
		let y = Math.min(e.y, window.innerHeight - ((cm?.clientHeight ?? 0) + pad));
		context = { left: x, top: y, show: true };
	};

	const hideContextMenu = () => {
		context = { ...DEFAULT_PLACEMENT, show: false };
	};

	$effect(() => {
		// Svelte 5 way to handle global window listeners reactively if needed,
		// or keep it in onMount inside the layout.
		window.addEventListener('mousedown', hideContextMenu);
		window.addEventListener('contextmenu', contextMenu);

		return () => {
			window.removeEventListener('mousedown', hideContextMenu);
			window.removeEventListener('contextmenu', contextMenu);
		};
	});
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<div class="flex h-screen w-screen flex-col gap-2 bg-black p-2">
	<!-- This renders whichever page.svelte is active -->
	{@render children()}
</div>

<ContextMenu
	bind:left={context.left}
	bind:top={context.top}
	bind:show={context.show}
	bind:data={contextButtonData}
/>
