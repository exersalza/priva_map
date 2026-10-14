<script lang="ts">
	import { getContext, onMount, setContext } from 'svelte';

	const registerContextMenu =
		getContext<{ update: (buttons: any) => void }>('registerContextMenu');

    onMount(() => {
        registerContextMenu.update([
            {text: "test", f: () => console.log("help")}
        ]);
    });

	onMount(() => {});
</script>

<div class="text-white">HAHAHAHHAHH</div>
