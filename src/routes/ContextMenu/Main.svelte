<script lang="ts">
    import { clickOutside } from 'svelte-use-click-outside';
    
    export let showContextMenu: boolean;
    export let contextMenuPosition: number[];
</script>

<main style="left: {contextMenuPosition[0]}px; top: {contextMenuPosition[1]}px;" use:clickOutside={() => showContextMenu = false}>
    <slot></slot>
</main>

<style>
    main {
        width: 200px;
        height: fit-content;

        border-radius: 8px;
        border: 1px solid var(--gray2);

        padding: 6px;

        background: var(--gray1);
        position: absolute;

        display: flex;
        flex-direction: column;
        gap: 0px;

        box-shadow: 0px 10px 23px rgba(0, 0, 0, 0.04);
        animation: enter .075s ease-in-out;
    }

    @keyframes enter {
        0% {
            transform: translateY(-5px);
        }

        100% {
            transform: translateY(0px);
        }
    }
</style>