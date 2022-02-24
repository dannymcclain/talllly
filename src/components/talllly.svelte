<script>
    export let talllly;
    import { tallllys } from "../stores.js";

    function updateCount(type, talllly){
        let count = talllly.count;
        let emoji = talllly.emoji;
        let id = talllly.id;
        let title = talllly.title;

        let newTallllies = Array.from($tallllys);

        var actions = {
            'deincrement': function() {
                if (talllly.id === id){
                    if (talllly.count > 0){
                        let lowerCount = (talllly.count - 1);
                        talllly.count = lowerCount;
                    } else {
                        talllly.count = 0;
                    }
                }
                $tallllys = newTallllies;
                tallllys.update(current => newTallllies);
                localStorage.setItem("tallllys", JSON.stringify($tallllys));
            },
            'increment': function() {
                if (talllly.id === id){
                    let higherCount = (talllly.count + 1);
                    talllly.count = higherCount;
                }
                $tallllys = newTallllies;
                tallllys.update(current => newTallllies);
                localStorage.setItem("tallllys", JSON.stringify($tallllys));
            }
        }
        return actions[type]();
    }
</script>

<h2>{talllly.emoji}</h2>
<h3>{talllly.count}</h3>
<p>{talllly.title}</p>
<button on:click={() => updateCount('deincrement', talllly)}>-</button>
<button on:click={() => updateCount('increment', talllly)}>+</button>

<style>
    h2 {
        font-family: "Apple Color Emoji";
    }
</style>