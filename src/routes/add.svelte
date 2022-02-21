<script>
    import { emoji } from "../stores.js";
    import { tallllys } from "../stores.js";

    let title = 'Hi';
    let titleEmoji = 'Yo';
    let visible = false;

    function log() {
        console.log(titleEmoji, title);
    }
</script>
<section>
    <p>{title}</p>
    <p>{titleEmoji}</p>
</section>
<form>
    <input type="text" bind:value={title} />
</form>
<button on:click={() => visible = true}>Show emoji</button>
<button on:click={log}>Log</button>
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
    transform: scale(1);
    transition: transform 200ms cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.emoji button:hover {
    transform: scale(1.25);
}
</style>