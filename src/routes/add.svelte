<script lang='ts'>
    import { emoji } from "../stores.js";
    import { tallllys } from "../stores.js";
    import { v4 as uuidv4 } from 'uuid';
    import { goto } from '$app/navigation';
    import { fly } from 'svelte/transition';
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

    function selectEmoji(emo) {
        titleEmoji = emo;
        visible = false;
    }

    onMount(() => {
            randomEmoji = $emoji[getRandomNum($emoji.length)]
            titleEmoji = randomEmoji;
    });
</script>
<svelte:window on:keydown={handleKeydown}/>

<div>
    <input type="text" bind:value={title} />
</div>
<button on:click={() => visible = true}>{titleEmoji}</button>
<button on:click={createTally}>Add</button>
<button on:click={() => goto('/')}>Cancel</button>

{#if visible}
    <div transition:fly={{y: 100, duration: 300}} class="popup">
        
        <button on:click={() => visible = false}>x</button>
        <section class="emoji">
            {#each $emoji as emo}
            <button on:click={() => selectEmoji(emo)}>{emo}</button>
            {/each}
        </section>
    </div>
{/if}

<style>
.popup {
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    max-width: 100vw;
    max-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    background: red;
}
.emoji {
    display: flex;
    flex-wrap: wrap;
    gap: .5rem;
    padding: 2rem;
    overflow-y: scroll;
    width: 100%;
    height: 100%;
    margin: auto;
    background: white;
}

.emoji button {
    font-family: "Apple Color Emoji";
    font-size: 1.5rem;
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