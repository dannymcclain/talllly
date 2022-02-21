<script>
    export let talllly;

    import { tallllys } from "../stores.js";

    const increment = function(talllly) {
        let count = talllly.count;
        let emoji = talllly.emoji;
        let id = talllly.id;
        let title = talllly.title;

        let newTallllies = Array.from($tallllys);
        newTallllies.forEach(function(talllly){
            if (talllly.id === id){
                let higherCount = (talllly.count + 1);
                talllly.count = higherCount;
                console.log(talllly.emoji, talllly.count);
            }
            $tallllys = newTallllies;
        })
    }

</script>

<h3>{talllly.title} <small>({talllly.id})</small></h3>
        <h2>
            {#each Array(talllly.count) as _, i}
            {talllly.emoji}
            {/each}
        </h2>
        <p>{talllly.count}</p>
        <button on:click={() => increment(talllly)}>+</button>