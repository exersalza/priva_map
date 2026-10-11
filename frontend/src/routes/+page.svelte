<script lang="ts">
	import { onMount } from "svelte";
	import MainMenu from "../comp/MainMenu.svelte";
	import Map from "../comp/Map.svelte";
	import ContextMenu from "../comp/ContextMenu.svelte";

    let context = $state({left: 0, top: 0, show: false});
    let contextButtonData = $state([
        {text: "Save Coords", f: saveCoords}
    ]);

    function saveCoords() {
        console.log("AAHHHHHHHHH");
        context = {...context, show: false};
    }


    const contextMenu = (e: PointerEvent) => {
        // if (!e.target.parentElement.id === "map-wrapper") {

            e.preventDefault();
        // }

        context = {left: e.x, top: e.y, show: true};
    };

    const hideContextMenu = () => {
        context = {left: 0, top: 0, show: false}
    }


    onMount(() => {
        window.addEventListener("mousedown", hideContextMenu);
        window.addEventListener("contextmenu", contextMenu);

        return () => {
            window.removeEventListener("contextmenu", contextMenu)
            window.removeEventListener("mousedown", hideContextMenu);
        }
    });
</script>


<div class="h-screen w-screen bg-black p-2 flex flex-col gap-2">
    <MainMenu />

    <Map />
</div>

<ContextMenu
    bind:left={context.left}
    bind:top={context.top}
    bind:show={context.show}
    bind:data={contextButtonData}
    />
