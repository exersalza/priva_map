<script lang="ts">
	import Borderd from './Borderd.svelte';

	export type ButtonVariant = 'primary' | 'secondary' | 'danger';

	let {
		children,
		type = 'primary',
		onclick = () => {}
	}: { children: any; type: ButtonVariant; onclick: () => void } = $props();
</script>

<Borderd>
	<button
		class="flex size-full items-center justify-center px-1 text-white uppercase hover:bg-white hover:text-black"
		{onclick}
	>
		{#if children}
			{@render children()}
		{:else}
			<p>Here should be text</p>
		{/if}
	</button>
</Borderd>
