<script lang="ts">
    import { Cross1 } from "radix-icons-svelte";
    
    export let title: string;
    export let description: string;
</script>

<main>
    <h1>{title}</h1>
    <p>{description}</p>
</main>

<style>
    main {
        width: 100%;
        height: fit-content;
        min-width: 64px;

        display: flex;
        flex-direction: column;
        gap: 4px;
        padding: 16px;
        padding-left: 24px;
    }

    h1 {
        font-family: Inter;
        font-size: 14px;
        font-weight: 600;
        color: var(--gray12);
    }

    p {
        font-family: Inter;
        font-size: 14px;
        font-weight: normal;
        color: var(--gray11);
    }
</style>