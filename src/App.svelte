<script lang="ts">
	import AddLocation from "./lib/AddLocation.svelte";
import Card from "./lib/Card.svelte";
	import { locations } from './lib/store';
	let locationsValue = [] as string[];
	locations.subscribe(value => {
		locationsValue = value;
	});
</script>

<div class="container">
	<h1>Weather App</h1>
	<AddLocation />
	<div class="row my-3">
		{ #each locationsValue as location}
			<Card place={location} />
		{/each}
	</div>
</div>