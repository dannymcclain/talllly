<script lang='ts'>
    import { emoji } from "../stores.js";
    import { tallllys } from "../stores.js";
    import { v4 as uuidv4 } from 'uuid';
    import { goto } from '$app/navigation';
    import { onMount } from 'svelte';

    let randomEmoji:string;

    let title;
    let titleEmoji;
    let visible = false;

    let key;

    function getRandomNum(num) {
        return Math.floor(Math.random() * num)
    }
  
    function createTally() {
        if (title){
            let newTalllly = {
                emoji: titleEmoji,
                title: title,
                count: 1,
                id: uuidv4()
            }
        
            let newTallllies = Array.from($tallllys);
    
            newTallllies.unshift(newTalllly);
    
            tallllys.update(current => newTallllies);

            localStorage.setItem("tallllys", JSON.stringify($tallllys));

            goto('/');
        } else {
            return;
        }
    }

    function handleKeydown(event) {
		key = event.key;
        if (key === 'Enter'){
            createTally();
        } else if (key === 'Escape') {
            goto('/')
        } else {
            return;
        }
	}

    onMount(() => {
            randomEmoji = $emoji[getRandomNum($emoji.length)]
            titleEmoji = randomEmoji;
    });
</script>
<svelte:window on:keydown={handleKeydown}/>
<!-- <section>
    <p>{title}</p>
    <p>{titleEmoji}</p>
</section> -->
<div>
    <input type="text" bind:value={title} />
</div>
<button on:click={() => visible = true}>{titleEmoji}</button>
<button on:click={createTally}>Add</button>
<button on:click={() => goto('/')}>Cancel</button>

{#if visible}
    <section class="emoji">
        {#each $emoji as emo}
        <button on:click={() => titleEmoji = emo}>{emo}</button>
        {/each}
    </section>
{/if}

<style>
.emoji {
    display: flex;
    flex-wrap: wrap;
    gap: .5rem;
    height: 400px;
    overflow-y: scroll;
}

.emoji button {
    font-family: "Apple Color Emoji";
    font-size: 2rem;
    outline: none;
    /* padding: .5rem; */
    margin: 0;
    border: none;
    background: transparent;
    /* transform: scale(1);
    transition: transform 200ms cubic-bezier(0.175, 0.885, 0.32, 1.275); */
}

.emoji button:hover {
    /* transform: scale(1.25); */
    background: #f5f5f5;
}
</style>