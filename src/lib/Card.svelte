<script lang="ts">
    import { onMount } from "svelte";
    import { locations } from '../lib/store';
    export let place: string;
    const apiKey = import.meta.env.VITE_WEATHER_API_KEY;
    let data;
    onMount(async () => {
        try {
            const res = await fetch(
                `https://api.weatherapi.com/v1/current.json?key=${apiKey}&q=${place}&aqi=no`
            );
            data = await res.json();
            if(data.error) removeItem();
        } catch (e) {
            console.log(e);
        }
    });

    const removeItem = () => {
        locations.update(arr => {
            return arr.filter(location => location !== place);
        })
    }
</script>

<div class="card col-3 m-1">
    <div class="card-body">
        <h5 class="card-title">
            {data?.location ? `${data.location.name}, ${data.location.region}` : "Loading..."}
        </h5>
        <p class="card-text">
            {data?.current ? `${data.current.condition.text}, ${Math.round(data.current.temp_f)}` : "Loading..."}
        </p>
        <button class="btn btn-danger" on:click={removeItem}>Remove item</button>
    </div>
</div>
