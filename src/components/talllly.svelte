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

<h2>{talllly.emoji}</h2>
<h3>{talllly.count}</h3>
<p>{talllly.title}</p>
<button on:click={() => increment(talllly)}>+</button>