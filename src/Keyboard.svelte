<script>
    export let buttons;
</script>

<div class="keyboard">
    {#each buttons as button}
        <button id={button.id} on:click={button.action}>{button.value}</button>
    {/each}
</div>

<style>
    .keyboard {
        background-color: black;
        width: 290px;
        display: grid;
        grid-template-columns: repeat(4, 22%);
        grid-auto-rows: max-content;
        grid-gap: 10px;
        cursor: pointer;
        user-select: none;
    }

    button {
        color: white;
        height: 64px;
        font-weight: 600;
        font-size: 1.2em;
        cursor: pointer;
        margin: 0px;
        background-color: #444444;
        border-radius: 32px;
        border-width: 0px;
    }

    #num-0 {
        grid-column: 1 / span 2;
    }

    button:empty {
        background-color: black;
    }
</style>
