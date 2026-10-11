<script lang="ts">
	import Borderd from "./Borderd.svelte";

    export type ButtonVariant = 'primary' | 'secondary' | 'danger';

    let {children, type, onclick}: {children: any, type: ButtonVariant, onclick: () => void} = $props();


</script>

<Borderd>
    <button class="text-white flex items-center justify-center size-full hover:bg-white hover:text-black"
        onclick={onclick}>
        {#if children}
            {@render children()}
        {:else}
            <p>Here should be text</p>
        {/if}
    </button>
</Borderd>
