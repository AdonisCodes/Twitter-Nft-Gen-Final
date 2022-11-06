<script>

    import { fade, fly } from 'svelte/transition';

    import { createEventDispatcher } from "svelte";
    let dispatch = createEventDispatcher()
    let red = 1
    let green = 1
    let blue = 1

    function colourHandler() {
        dispatch('colourChange', {colour:{r: red, g: green, b: blue}})
    }

    let openBool = true
</script>


{#if openBool }

<button on:click={() => openBool = !openBool} class="expandBtn" style="margin-top: -0vh ;">
    <span class="material-symbols-outlined">
        expand_less
    </span>
</button>
<h1>Colour Picker</h1>
{:else}

<button on:click={() => openBool = !openBool} class="expandBtn">
    <span class="material-symbols-outlined">
        expand_more
    </span>
</button>

{/if}


{#if openBool }
<div transition:fade="{{duration: 100 }}" class="Container" style="margin-top: -0vh ;">

            <div >
                <input transition:fly="{{y: -10, duration: 100 }}" class="slider" on:change={() =>colourHandler()} bind:value={red} type="range" min="1" max="255" />
                <input transition:fly="{{y: -10, duration: 100}}" class="slider" on:change={() =>colourHandler()} bind:value={green} type="range" min="1" max="255" />
                <input transition:fly="{{y: -10, duration: 100 }}" class="slider" on:change={() =>colourHandler()} bind:value={blue} type="range" min="1" max="255" />
            </div>
    
            <div  transition:fly="{{y: -10, duration: 200 }}" class="Container colourDisplay" style="background-color: rgb({red}, {green}, {blue}) ;"></div>        
</div>

{/if}

<style>

    * {
        margin: none;
        padding: none;
    }

    div {
        display: grid;
        width: 25vh;
        border-radius: 1vh;
    }
    .Container{
        display: grid;
        grid-template-columns: 1fr 1fr;
        column-gap: 1vh;
    }
    .colourDisplay {
        width: 16vh;
        height: 16vh;
    }

    h1 {
        display: inline;
    }
</style>