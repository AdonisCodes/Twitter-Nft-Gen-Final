<script>
    // @ts-nocheck
    
        import rough from "roughjs";
        import Viewport from 'svelte-viewport-info'
    
    // npm i roughjs@4.0.4
    // https://roughjs.com/
    export let fillColour = 'rgba(255,0,200,1)';
    export let drag = false;
    export let shapeType = 'rectangle';
    export let shapeSize = {width: 100, height: 100};

    let roughSvg;
    let canvas;
    let mousePos = {x:100, y:100};
    let shapeCount = 5
    let shapes = []

    $: newRectXY =  {x:(mousePos.x - (0.14 * Viewport.Height)) , y: (mousePos.y - (0.17 * Viewport.Height))}
    $: newXYCirc = {x: mousePos.x - (0.05 * Viewport.Height), y: mousePos.y - (0.1 * Viewport.Height) - ( shapeSize.width  / Infinity)}

    function rectangle(x, y, width , height, style, colour) {
            roughSvg = rough.canvas(canvas); 
            const rect = roughSvg.rectangle(x, y, width, height, {  // x, y, width, height
            fill: colour,
            fillStyle: style // solid fill
    })}

    function circle(x, y, width, style, colour) {
            roughSvg = rough.canvas(canvas); 
            const rect = roughSvg.circle(x, y, width, {  // x, y, width, height
            fill: colour,
            fillStyle: style // solid fill
            });
    }

    function line(x, y, width, height) {
            roughSvg = rough.canvas(canvas); 
            console.log(shapeSize)
            const rect = roughSvg.line(x, y, width, height)
    }


    function reDrawShapes() {
        let ctx = canvas.getContext('2d')
         ctx.clearRect(0, 0, canvas.width, canvas.height);

        for (let i = 0; i < shapes.length; i++) {

            if (shapes[i].shape == 'Rectangle') {
                rectangle(shapes[i].x, shapes[i].y, shapes[i].height, shapes[i].width, shapes[i].style, shapes[i].colour)
            }
            if (shapes[i].shape == 'Circle') {
                circle(shapes[i].x, shapes[i].y, shapes[i].width, shapes[i].style, shapes[i].colour)
            }
            if (shapes[i].shape == 'Line') {
                line(shapes[i].x, shapes[i].y, shapes[i].width, shapes[i].height)
            }
        }
    }
    

    function action(canvas) {
        if (drag) {
            return
        }

        if (shapeCount <= 0 ) {
            return
        }

        if (shapeType == 'circle') {
            let newCircle = {shape: 'Circle', x: newXYCirc.x, y: newXYCirc.y, width: shapeSize.width, style: 'dots', colour: fillColour}
            shapes.push(newCircle)
            circle(newCircle.x, newCircle.y, newCircle.width, newCircle.style, newCircle.colour)
        }

        if (shapeType == 'rectangle') {
            let newRect = {shape: 'Rectangle', x:newRectXY.x, y: newRectXY.y, width: shapeSize.width, height: shapeSize.height, style: 'dots', colour: fillColour}
            shapes.push(newRect)
            rectangle(newRect.x, newRect.y, newRect.height, newRect.width, newRect.style, newRect.colour)
        }
    
        if (shapeType == 'line') {
            let newRect = {shape: 'Line', x:newRectXY.x, y: newRectXY.y, width: shapeSize.width, height: shapeSize.height, style: 'dots', colour: fillColour}
            shapes.push(newRect)
            line(newRect.x, newRect.y, newRect.height, newRect.width)
        }
    
        shapeCount--
    }

    function setMouseVar(e) {
    mousePos.x = e.clientX 
    mousePos.y = e.clientY}
    </script>
    
<div>
    <canvas on:mousemove={setMouseVar} on:click={() =>  action(canvas)} width="250" height="250" bind:this={canvas}></canvas>
</div>

<style>

 :global(*) {
    box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px, rgba(0, 0, 0, 0.5) 0px 1px 3px -1px;
    }

    canvas {
        background-color: whitesmoke;
        height: 250px;
        width: 250px;
    }
</style>