<script lang="ts">
	import MainMenu from '../comp/MainMenu.svelte';
	import Map from '../comp/Map.svelte';
	import type { Map as LLMap } from 'leaflet';

	let coords = $state({ home: [53.580013, 10.04076] });
	let mapInstance: LLMap | undefined = $state();
</script>

<MainMenu bind:mapInstance />

<Map bind:coords bind:mapInstance />
