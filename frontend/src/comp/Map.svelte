<script lang="ts">
	import Borderd from './Borderd.svelte';
	import { Map, TileLayer, Marker, Popup } from 'sveaflet';
	import type { MapOptions, Map as LLMap, LeafletMouseEvent } from 'leaflet';
	import { DEFAULT_PLACEMENT } from './ContextMenu.svelte';
	import { getContext, onMount, setContext } from 'svelte';

	let { coords = $bindable({ home: [53.580013, 10.04076] }), mapInstance = $bindable() } = $props();

	const registerContextMenu = getContext<{ update: (buttons: any) => void }>('registerContextMenu');

	onMount(() => {
		registerContextMenu.update([
			{ text: 'Save Coords', f: saveCoords },
			{ text: 'Set Home', f: setHome }
		]);
	});

	let mapOptions: MapOptions = {
		center: coords.home,
		zoom: 18,
		maxZoom: 18,
		minZoom: 12,
		attributionControl: false
	};

    let lastCoords;

	let context = $state({ ...DEFAULT_PLACEMENT, show: false });

	function hideCM() {
		context = { ...context, show: false };
	}

	function saveCoords() {
        console.log(lastCoords);
		hideCM();
	}

	function setHome() {
		hideCM();
	}

	$effect(() => {
		if (!mapInstance) return;

		mapInstance.on('contextmenu', (e: LeafletMouseEvent) => {
			const { lat, lng } = e.latlng;

			console.log({ lat, lng });
            lastCoords = {lat, lng};
			console.log(`Right-clicked at: Lat ${lat}, Lng ${lng}`);
		});
	});
</script>

<Borderd className="flex-1 min-h-0 w-full h-full" id="map-wrapper">
	<Map options={mapOptions} bind:instance={mapInstance}>
		<TileLayer url={'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png'} />
	</Map>
</Borderd>

<!--
<style>
  :global(.leaflet-tile-pane) {
    filter: brightness(0.7) invert(1) contrast(2) hue-rotate(200deg) saturate(0.6);
  }
</style> -->

<!--
dark mode, but looks kinda trash
-->
