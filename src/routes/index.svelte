<script>
    function randomColor() {
        return '#' + Math.floor(Math.random()*16777215).toString(16)
    }

    let number = 3

    function addSquare() {
        number++
    }
    function clear() {
        number= 0
    }

    let size = 1
    let rotation = 1
    let translate = 1
</script>


<div id="controls">
    <button id='add-square' on:click={addSquare}>Add Square</button>
    <button id="clear" on:click={clear}>🔁</button>

    <div id="sliders">
        <div class="slider">
            <label for="size">size {size}</label>
            <input type="range" bind:value={size} min="0.1" max="10">
        </div>
        
        <div class="slider">
            <label for="rotation">rotation {rotation}</label>
            <input type="range" bind:value={rotation} min="0.1" max="10" step="0.01">
        </div>
        
        <div class="slider">
            <label for="translate">translate {translate}</label>
            <input type="range" bind:value={translate} min="0.1" max="20" step="0.01">
        </div>
    </div>
</div>


<div id="svg-container">
    {#each Array(number) as color, i}
        <div id="svg-wrapper">
            <svg
                width="50"
                viewBox="0 0 220 100"
                xmlns="http://www.w3.org/2000/svg"
                style="transform: translate({i * translate}px, {i * translate}px) scale({(i * 1.01) * size}) rotate({i * 15 * rotation}deg);"
            >
                <rect fill="hsl({255 - (i*5)}, 100%, 50%)" width="100" height="100" />
            </svg>
        </div>
    {/each}
</div>

<style>
    :global(body) {
        background: rgb(0, 0, 0);
    }
    #controls {
        position: relative;
        z-index: 10;
        display: flex;
    }
    #add-square {
        background-color:rgb(119, 119, 165);
        color: white;
        font-size: 25px;
        width: 100px;
        height: 100px;
    }
    #clear {
        background: transparent;
        font-size: 25px;
        border: none;
        width: 35px;
        height: 35px;
        margin: auto 10px;
    }
    #sliders {
        display: flex;
        flex-direction: column;
        margin-left: 100px;
    }
    label {
        color: white;
        width: 200px;
    }
    .slider {
        width: 300px;
    }
    .slider input {
        width: 100%;
    }
    #svg-container {
        position: relative;
        padding-top: 25vh;
        margin: auto;
        width: 0;
        height: 0;
        transform: translateY(25vh);
    }
    #svg-wrapper {
        transform-origin: 50%;
        z-index: 5;
        pointer-events: none;
        position: absolute;
        margin: auto;
        bottom: 0;
        right: 0;
        left: 0;
        top: 0;
        animation: 10s infinite spin;
    }
    @keyframes spin {
        0% {
            transform: rotate(0deg)
        }
        100% {
            transform: rotate(360deg)
        }
    }
    svg {
        backface-visibility: hidden;
    }
</style>