<script lang="ts">
    import Talllly from '../components/Talllly.svelte';
    import { tallllys } from "../stores.js";
    import { onMount } from 'svelte';
    import { goto } from '$app/navigation';

    let key;

    function handleKeydown(event) {
		key = event.key;
        if (event.shiftKey && key === '+'){
            goto('/add');
        } else {
            return
        }
	}

    onMount(() => {
            const data = JSON.parse(localStorage.getItem("tallllys"));
            if (data) {
            tallllys.update(entry => data);
        }
    });
</script>

<svelte:window on:keydown={handleKeydown}/>

<h1>Tally</h1>
<a href="/add">Add</a>
<section>
    {#each $tallllys as talllly}
        <Talllly {talllly} />
    {/each}
</section>

<style>

</style>