<script lang="ts">
	import Borderd from "./Borderd.svelte";
	import { Map, TileLayer, Marker, Popup } from 'sveaflet';
    import type {MapOptions, Map as LLMap, LeafletMouseEvent} from "leaflet";

    let mapOptions: MapOptions = {
			center: [53.580013, 10.040760],
			zoom: 18,
            maxZoom: 18,
            minZoom: 12,
            attributionControl: false
	};

    let mapInstance: LLMap | undefined = $state();

    $effect(() => {
        if (!mapInstance) return;

        mapInstance.on('contextmenu', (e: LeafletMouseEvent) => {
            const { lat, lng } = e.latlng;

            console.log({ lat, lng });
            console.log(`Right-clicked at: Lat ${lat}, Lng ${lng}`);
          });

    });

</script>

<Borderd className="flex-1 min-h-0 w-full h-full" id="map-wrapper">
    <Map
        options={mapOptions}
        bind:instance={mapInstance}
	>
		<TileLayer url={'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png'} />
		<!-- <TileLayer url={'https://basemaps.cartocdn.com/rastertiles/voyager/{z}/{x}/{y}.png?key=cb1_4h7b_1_65bf21ba57930a8fd79de9cd'} /> -->
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
