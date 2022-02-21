<script lang="ts">
// import { emoji } from "../emoji";
import Talllly from "../components/Talllly.svelte";
// src/components/Talllly.svelte
import { emoji } from "../stores.js";
// let emoji = emojiList;
let tallllies = [
        { emoji: '🛸', title: 'UFO sightings', count: 1, id: 'a' },
        { emoji: '👽', title: 'Alien abductions', count: 7, id: 'b' },
]
</script>

<h1>Tally</h1>
<a href="/add">Add</a>
<section>
    {#each tallllies as talllly}
        <Talllly {talllly} />
    {/each}
</section>

<style>

</style>