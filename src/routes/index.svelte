<script lang="ts">
    import Talllly from '../components/Talllly.svelte';
    import { tallllys } from "../stores.js";
</script>

<h1>Tally</h1>
<a href="/add">Add</a>
<section>
    {#each $tallllys as talllly}
        <Talllly {talllly} />
    {/each}
</section>

<style>

</style>