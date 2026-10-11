<script module lang="ts">
    export type Data = {
        text: string,
        f: () => void
    }
</script>

<script lang="ts">
	import Borderd from "./Borderd.svelte";
	import Button from "./Button.svelte";

    let {
        left = $bindable(0),
        top = $bindable(0),
        show = $bindable(false),
        data = $bindable([] as Data[])
    } = $props();

</script>

<Borderd
    className={"z-[9999] absolute bg-black"}
    style="left: {left}px;top: {top}px;opacity: {Number(show)}">
    <div class="w-32" onmousedown={(e) => e.stopPropagation()}>
        {#each data as entry}
            <Button type="primary" onclick={entry.f}>{entry.text}</Button>
        {/each}
    </div>
</Borderd>
