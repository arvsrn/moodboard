<script lang="ts">
    export let style: 'danger' | 'normal' = 'normal';
    export let secondaryButtonLabel: string;
    export let primaryButtonLabel: string;
    export let secondaryButtonCallback: () => void;
    export let primaryButtonCallback: () => void;
</script>

<main>
    <button class="secondary" on:click={secondaryButtonCallback}>{secondaryButtonLabel}</button>
    <button class="{style}" on:click={primaryButtonCallback}>{primaryButtonLabel}</button>
</main>

<svelte:window on:keydown={e => {
    if (e.key === 'Escape') secondaryButtonCallback();
    else if (e.key === 'Enter') primaryButtonCallback();
}} />

<style>
    main {
        width: 100%;
        height: fit-content;
        min-width: 64px;

        display: flex;
        flex-direction: row;
        justify-content: flex-end;
        align-items: center;
        padding: 24px;
        gap: 8px;
    }

    button {
        height: 32px;
        width: fit-content;
        font-weight: 500;
        font-size: 13px;

        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
        padding: 12px;
        cursor: pointer;
        border-radius: 8px;
        outline: none;

        transition: transform 0.1s ease-in-out;
    }

    button.secondary {
        background: var(--gray2);
        border: 1px solid var(--gray3);
        color: var(--gray12);
    }

    button.danger {
        border: none;
        background-color: #E5484D;
        color: var(--gray12); 
    }

    button.normal {
        border: none;
        background-color: #0091FF;
        color: var(--gray12);
    }

    button:hover {
        transform: scale(1.05);
    }

    button:active {
        transform: scale(0.98);
    }
</style>