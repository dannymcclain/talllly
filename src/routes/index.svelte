<script>

let tallllies = [
        { emoji: '🛸', title: 'UFO sightings', count: 1, id: 'a' },
        { emoji: '👽', title: 'Alien abductions', count: 7, id: 'b' },
]

const increment = function(data) {
    let count = data.count;
    let emoji = data.emoji;
    let id = data.id;
    let title = data.title;
    let newTallllies = Array.from(tallllies);
    newTallllies.forEach(function(data){
        if (data.id === id){
            let higherCount = (data.count + 1);
            data.count = higherCount;
            console.log(data.emoji, data.count);
        }
        tallllies = newTallllies;
    })
}
</script>

<h1>Tally</h1>

<section>
    {#each tallllies as talllly}
        <h2>{talllly.emoji}</h2>
        <h3>{talllly.title} <small>({talllly.id})</small></h3>
        <p>{talllly.count}</p>
        <button on:click={() => increment(talllly)}>+</button>
    {/each}
</section>

<style>

</style>