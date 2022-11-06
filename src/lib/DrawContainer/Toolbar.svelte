<script>
    import ColourPicker from "./ToolBar/ColourPicker.svelte";
    import ShapePicker from "./ToolBar/ShapePicker.svelte";
    import Style from "./ToolBar/Style.svelte";
    import {createEventDispatcher} from 'svelte'

    let drag = false
    let disPatch = createEventDispatcher()

    function handleDrag() {
        drag = !drag
        disPatch('dragChange', drag)
    }
</script>

<div>
    {#if drag == false}
    <button on:click={() => handleDrag()} class="expandBtn" style="margin-top: -0vh ; padding">
        <span class="material-symbols-outlined">
            pan_tool
        </span>
    </button>
    {:else}
    <button on:click={() => handleDrag()} class="expandBtn" style="margin-top: -0vh ; background-color: #04AA6D;">
        <span class="material-symbols-outlined">
            pan_tool
        </span>
    </button>
    {/if}

    <ColourPicker on:colourChange/>

    <Style />

    <ShapePicker on:shapeChange on:heightChange/>
</div>

<style>
    button {
        background-color: rgba(1, 0, 37, 0.8);
        color: aliceblue;
        align-items: center;
    }
</style>