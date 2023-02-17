<script lang="ts">
    export let style: 'danger' | 'normal' = 'normal';
    export let secondaryButtonLabel: string;
    export let primaryButtonLabel: string;
    export let secondaryButtonCallback: () => void;
    export let primaryButtonCallback: () => void;
</script>

<main>
    <div style="margin-left:auto;display:flex;flex-direction:row;gap:8px;">
        <button class="secondary" on:click={secondaryButtonCallback}>{secondaryButtonLabel}</button>
        <button class="{style}" on:click={primaryButtonCallback}>{primaryButtonLabel}</button>
    </div>
</main>

<style>
    main {
        width: 100%;
        height: fit-content;
        min-width: 64px;

        display: flex;
        flex-direction: row;
        padding: 16px;
        padding-left: 24px;
        padding-top: 0px;
        align-items: center;
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
        border: 1px solid var(--gray6);
        background-color: var(--gray2);
        color: var(--gray11);
    }

    button.danger {
        border: none;
        background-color: #FF2C2C;
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