<script lang="ts">
    import { onMount } from "svelte";
    import ContextMenu from "./ContextMenu/Main.svelte";
    import Option from "./ContextMenu/Option.svelte";

    const UNIT = 25;

    export let position: [number, number];
    export let size: [string, string];
    export let style: 'normal' | 'twitter' = 'normal';
    export let offset: [number, number];

    let width: string = size[0];
    let height: string = size[1];

    let grabbing: boolean = false;
    let card: HTMLElement;
    let lastPosition: [number, number];
    let deltaX: number;

    let pos1: number, pos2: number, pos3: number, pos4: number;
    let showContextMenu: boolean = false;
    let contextMenuPosition: [number, number] = [0, 0];

    const every50ms = () => {
        if (lastPosition)
            deltaX = ((card.offsetLeft - pos1) / UNIT) - lastPosition[0];

        lastPosition = [(card.offsetLeft - pos1) / UNIT, (card.offsetTop - pos2) / UNIT];
        setTimeout(every50ms, 50);
    }

    onMount(() => every50ms()); 
</script>

{#if grabbing}
    <main class="shadow" style="position: absolute; left: {(Math.round(position[0]) * UNIT) + offset[0]}px; top: {(Math.round(position[1]) * UNIT) + offset[1]}px; width: {width}; height: {height};"></main>
{/if}

<main bind:this={card} style={
    grabbing ? 
    `position: absolute; left: ${(position[0] * UNIT) + offset[0]}px; top: ${(position[1] * UNIT) + offset[1]}px; width: ${width}; height: ${height}; transform: rotateZ(${deltaX}deg);` :
    `position: absolute; left: ${(Math.round(position[0]) * UNIT) + offset[0]}px; top: ${(Math.round(position[1]) * UNIT) + offset[1]}px; width: ${width}; height: ${height};`
} class={style} class:grabbing={grabbing} on:mousedown={(e) => {
    if (e.button === 0) {
        grabbing = true;
        pos3 = e.clientX;
        pos4 = e.clientY;
    }
}} on:contextmenu|preventDefault={e => {
    contextMenuPosition = [e.clientX, e.clientY];
    showContextMenu = true;
}} on:touchstart={e => {
    grabbing = true;
    pos3 = e.changedTouches[0].pageX;
    pos4 = e.changedTouches[0].pageY;

    window.navigator.vibrate(100);
}}>
    <div class="container">
        <slot></slot>
    </div>
</main>

{#if showContextMenu}
<ContextMenu bind:showContextMenu={showContextMenu} bind:contextMenuPosition={contextMenuPosition}>
    <Option text="Delete" action={() => {}}></Option>
</ContextMenu>
{/if}

<svelte:window on:mouseup={() => grabbing = false} on:mousemove={(e) => {
    if (grabbing) {
        pos1 = pos3 - e.clientX;
        pos2 = pos4 - e.clientY;
        pos3 = e.clientX;
        pos4 = e.clientY;

        position = [(card.offsetLeft - pos1 - offset[0]) / UNIT, (card.offsetTop - pos2 - offset[1]) / UNIT];
    }
}} on:touchend={() => grabbing = false} on:touchmove={e => {
    if (grabbing) {
        pos1 = pos3 - e.changedTouches[0].pageX;
        pos2 = pos4 - e.changedTouches[0].pageY;
        pos3 = e.changedTouches[0].pageX;
        pos4 = e.changedTouches[0].pageY;

        position = [(card.offsetLeft - pos1) / UNIT, (card.offsetTop - pos2) / UNIT];
    }
}}></svelte:window>

<style>
    main {
        width: 400px;
        height: 400px;

        border-radius: 16px;

        cursor: grab;
        transition: box-shadow 0.1s ease-in, transform 0.1s ease-in;
        overflow: hidden;
        touch-action: none;
    }

    main.normal {
        background-color: var(--gray1);
        border: 1px solid var(--gray4);
    }

    main.twitter {
        background-color: #F5FAFE;
        border: 1px solid #E2E6EA;
    }

    div.container {
        width: 100%;
        height: 100%;

        position: relative;
    }

    main.shadow {
        border: none;
        background-color: var(--gray3);
    }

    main.grabbing {
        cursor: grabbing;
        box-shadow: 0px 0px 23px rgba(0, 0, 0, 0.03);
    }
</style>