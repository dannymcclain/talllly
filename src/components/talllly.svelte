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

    function editTalllly(tal) {
        console.log(tal)
    }
</script>

<div class="talllly">
    <div class="content" on:click={() => editTalllly(talllly)}>
        <h2>{talllly.emoji}</h2>
        <div class="details">
            <h3>{talllly.count}</h3>
            <p>{talllly.title}</p>
        </div>
    </div>
    <div class="actions">
        <button on:click={() => updateCount('deincrement', talllly)}>-</button>
        <button on:click={() => updateCount('increment', talllly)}>+</button>
    </div>
</div>

<style>
    .talllly {
        margin-bottom: 0;
        display: flex;
        flex-direction: row;
        flex-wrap: nowrap;
        justify-content: space-between;
        align-items: center;
    }
    h2 {
        font-family: "Apple Color Emoji";
    }
    h3 {
        margin: 0;
        padding: 0;
        line-height: 1;
    }
    p {
        margin: 0;
        padding: 0;
        line-height: 1;
    }
    .content {
        display: flex;
        flex-direction: row;
        justify-content: flex-start;
        align-items: center;
        cursor: pointer;
        gap: 1rem;
    }
    .details {
        display: flex;
        flex-direction: column;
    }
</style>