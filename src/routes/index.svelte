<script>
// import { emoji } from "../emoji";
import { tallllys } from "../stores.js";
import { emoji } from "../stores.js";
// let emoji = emojiList;
let tallllies = [
        { emoji: '🛸', title: 'UFO sightings', count: 1, id: 'a' },
        { emoji: '👽', title: 'Alien abductions', count: 7, id: 'b' },
]

const increment = function(talllly) {
    let count = talllly.count;
    let emoji = talllly.emoji;
    let id = talllly.id;
    let title = talllly.title;
    let newTallllies = Array.from(tallllies);
    newTallllies.forEach(function(talllly){
        if (talllly.id === id){
            let higherCount = (talllly.count + 1);
            talllly.count = higherCount;
            console.log(talllly.emoji, talllly.count);
        }
        tallllies = newTallllies;
    })
}
</script>

<h1>Tally</h1>

<section>
    {#each tallllies as talllly}
        <h3>{talllly.title} <small>({talllly.id})</small></h3>
        <h2>
            {#each Array(talllly.count) as _, i}
            {talllly.emoji}
            {/each}
        </h2>
        <p>{talllly.count}</p>
        <button on:click={() => increment(talllly)}>+</button>
    {/each}
</section>
<section class="emoji">
    {#each $emoji as em, i}
        <p>{em}</p>
    {/each}
</section>
<style>
h2 {
    display: flex;
    flex-wrap: wrap;
}

.emoji {
    font-family: "Apple Color Emoji";
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
}
.emoji p {
    margin: 0;
    padding: 0;
    transform: scale(1);
    transition: transform 200ms cubic-bezier(0.175, 0.885, 0.32, 1.275);
}
.emoji p:hover {
    transform: scale(1.5);
}
</style>