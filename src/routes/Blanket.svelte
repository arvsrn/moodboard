<script lang="ts">
    export let onClick: () => void;
</script>

<main on:click|self={onClick}>
    <slot></slot>
</main>

<style>
    main {
        width: 100vw;
        height: 100vh;

        position: absolute;
        top: 0px;
        left: 0px;
        z-index: 5;

        display: flex;
        align-items: center;
        justify-content: center;
        
        background: rgba(0, 0, 0, 0.01);
        backdrop-filter: blur(10px);
    }
</style>