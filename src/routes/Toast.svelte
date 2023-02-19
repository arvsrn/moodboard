<script lang="ts">
    import { Cross1 } from "radix-icons-svelte";
    import { slide } from "svelte/transition";

    interface Toast {
        heading: string;
        description: string;
    }

    let notifications: Array<Toast> = [];

    export const addNotification = (notification: Toast) => {
        notifications = [...notifications, notification];
    };
</script>

<main>
    {#each notifications as notification, i} 
    <div transition:slide={{ duration: 85 }} class="toast" style="--index:{notifications.length - 1 - i};">
        <h1>{notification.heading}</h1>
        {#if notification.description}
        <p>{notification.description}</p>
        {/if}

        <div style="position:absolute;height:100%;aspect-ratio:1/1;right:0px;top:0px;display:flex;align-items:center;justify-content:center;">
            <button on:click={() => {
                notifications.splice(i, 1);
                notifications = notifications;
            }}>
                <Cross1></Cross1>
            </button>
        </div>
    </div>
    {/each}
</main>

<style>
    main {
        width: 350px;
        height: fit-content;

        position: absolute;
        bottom: 120px;
        right: 24px;

        display: flex;
        flex-direction: column;
        gap: 16px;
        z-index: 10;
    }

    div.toast {
        display: flex;
        flex-direction: column;
        gap: 4px;

        position: relative;

        background-color: var(--gray1);
        border: 1px solid var(--gray4);
        box-shadow: 0px 4px 12px rgba(0, 0, 0, 0.12);
        border-radius: 8px;

        padding: 16px;
        height: fit-content;
        width: 100%;

        transition: transform 0.2s ease-in-out, opacity 0.2s ease-in-out;
    }

    main:not(:hover) div.toast {
        transform: translateY(calc(105% * var(--index))) scale(calc(-1 * var(--index) * 0.05 + 1));
        opacity: calc(1 - (var(--index) - 2));
    }

    p, h1 {
        user-select: text;
    }

    h1 {
        font-family: Inter;
        font-size: 13px;
        font-weight: 500;

        color: var(--gray12);
    }

    p {
        font-family: Inter;
        font-size: 13px;
        font-weight: normal;

        color: var(--gray11);
    }

    button {
        background-color: transparent;
        border-radius: 8px;

        border: none;
        outline: none;
        cursor: pointer;

        display: flex;
        align-items: center;
        justify-content: center;

        width: 36px;
        height: 36px;

        color: var(--gray11);
        transition: background-color 0.15s ease-in-out;

        display: none; 
    }

    div.toast:hover button {
        display: block;
    }

    button:hover {
        background-color: var(--gray3);
    }
</style>