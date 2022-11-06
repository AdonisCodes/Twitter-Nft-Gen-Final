<script>
      import { fade, fly } from 'svelte/transition';
    import { createEventDispatcher } from "svelte";
    let disPatch = createEventDispatcher()

    $: size = {width: 100, height: 100}

    let shape_off = [ {shape: true, name: 'circle' } , { shape: false, name: 'rectangle' }, { shape: true, name: 'line' } ]

    function sizeHandler() {
        disPatch('heightChange', size)
        console.log(size)
    }


    function changeShape(shape) {
        shape_off[0].shape = true
        shape_off[1].shape = true
        shape_off[2].shape = true

        shape_off[Number(shape)].shape = false
        console.log(shape_off[shape])
        disPatch('shapeChange', shape_off)
    }

    let openBool = true
</script>

{#if openBool }

<button on:click={() => openBool = !openBool} class="expandBtn">
    <span class="material-symbols-outlined">
        expand_less
    </span>
</button>
<h1>Shape Config</h1>
{:else}

<button on:click={() => openBool = !openBool} class="expandBtn">
    <span class="material-symbols-outlined">
        expand_more
    </span>
</button>

{/if}

{#if openBool }
<div transition:fade="{{duration: 100 }}" class="Container MainContainer">
   <div transition:fly="{{y: -25, duration: 100 }}" class="width_height Container">
    <input class="slider" on:change={sizeHandler} bind:value={size.width} min="1" max="75"  type="range"/>
    <input class="slider" min="1" max="75"  bind:value={size.height} on:change={sizeHandler} type="range"/>
   </div>

    <div transition:fly="{{y: -25, duration: 200 }}" class="buttonDiv Container">
        <button  on:click={() => changeShape(0)} class="{shape_off[0].shape.toString()} button is-primary">
            <span class="material-symbols-outlined">
                circle
            </span>
        </button>

        <button on:click={() => changeShape(1)} class="{shape_off[1].shape.toString()} button is-primary">
            <span class="material-symbols-outlined">
                crop_square
            </span>
        </button>

        <button on:click={() => changeShape(2)} class="{shape_off[2].shape.toString()} button is-primary">
            <span class="material-symbols-outlined">
                timeline
            </span>
        </button>
    </div>
</div>
{/if}

<style> 
    .false {
        background-color: #04AA6D;
    }

    .true {
        background-color: rgba(1, 0, 37, 0.8);
    }

    .width_height {
        display: grid;
        row-gap: 1vh;
        width: 15vh;
        height: 10vh;
        margin: 0 0 ;
    }

    .buttonDiv {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        margin-left: -5vh;
        column-gap: 1vh;
        align-items: center;
        vertical-align: middle;
    }

    .button {
        width: 7vh;
        height: 7vh;
        margin-left: 0.5vh;
    }

    .MainContainer {
        display: grid;
        grid-template-columns: 1fr 1fr;
    }


</style>