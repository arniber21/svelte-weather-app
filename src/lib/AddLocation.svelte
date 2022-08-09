<script lang="ts">
    import { locations } from '../lib/store';
    let formValue;
    const handleSubmit = () => {
        locations.update(prev => {
            const update = [...prev, formValue];
            formValue = "";
            return update;
        })
    }
</script>

<form on:submit|preventDefault={handleSubmit}>
    <div class="mb-3">
        <input type="text" class="form-control" bind:value={formValue}/>
    </div>
    <button type="submit" class="btn btn-primary">Add Location</button>
</form>
