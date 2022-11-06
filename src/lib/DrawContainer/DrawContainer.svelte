<script>
    import Canvas from "./Canvas.svelte";
    import Toolbar from "./Toolbar.svelte";


    let shapeSize = {width: 100, height: 100}
    let shapeType;
    let fillColour = 'rgb(0, 0, 0,)'
    let drag;


</script>


<div>
    <Canvas {drag} {fillColour} {shapeType} {shapeSize}/>
    <Toolbar on:dragChange={(e) => {drag = e.detail, console.log(drag)}} on:colourChange={(e) => { fillColour = `rgb(${e.detail.colour.r}, ${e.detail.colour.g}, ${e.detail.colour.b})`}} on:shapeChange={(e) => {   for (let i = 0; i <= 2; i++) {if (e.detail[i].shape == false) {shapeType = e.detail[i].name}}}}  on:heightChange={(e) => {shapeSize =  e.detail}}/>
</div>

<style>
    div {
        display: grid;
        grid-template-rows: 1fr 1fr;
        row-gap: 0vh;
        justify-content: center;
        vertical-align: middle;
    }
</style>