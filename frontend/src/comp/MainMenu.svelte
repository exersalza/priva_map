<script lang="ts">
	import Borderd from './Borderd.svelte';
	import Button from './Button.svelte';
	import type {
		MapOptions,
		Map as LLMap,
		LeafletMouseEvent,
		LatLngExpression,
		ZoomPanOptions
	} from 'leaflet';

	let { mapInstance = $bindable() }: { mapInstance: LLMap | undefined } = $props();

	function moveTo(coords: LatLngExpression, zoom?: number) {
		if (!mapInstance) return;

		mapInstance.setView(coords, zoom ? zoom : 18, { animate: true });
	}
</script>

<Borderd>
	<div class="flex flex-col gap-1">
        <Borderd className="flex">
            <Button>map</Button>
        </Borderd>
		<div class="flex h-12 gap-1">
			<Button type="primary" onclick={() => moveTo([53.579489483342414, 10.050919889578797])}
				>home</Button
			>
		</div>
	</div>
</Borderd>
