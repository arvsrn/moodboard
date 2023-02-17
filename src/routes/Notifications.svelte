<script lang="ts">
    import { fade } from "svelte/transition";


    export let notifications: Array<string> = [];

    export const addNotification = (text: string) => {
        notifications.push(text);
        setTimeout(() => {
            notifications = notifications.splice(notifications.length - 1, 1);
        }, 1000);
        notifications = notifications;
    };
</script>

<main>
    {#each notifications.slice(-3) as notification}
        <div transition:fade class="notification">
            <p>{notification}</p>
        </div>
    {/each}
</main>

<style>
    main {
        width: 400px;
        height: fit-content;

        position: absolute;
        right: 0px;
        bottom: 0px;

        display: flex;
        flex-direction: column;
        gap: 16px;
        padding: 16px;
    }

    div.notification {
        background-color: var(--gray2);
        border: 1px solid var(--gray6);
        border-radius: 8px;

        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        padding: 16px;

        transition: transform 0.1s ease-in-out;
    }

    p {
        font-family: Inter;
        font-size: 14px;
        color: var(--gray12);

        width: 100%;
        height: fit-content;
    }

    main:not(:hover) div.notification:first-child:not(:only-child) {
        transform: scale(0.92) translateY(232%);
        z-index: 0;
    }

    main:not(:hover) div.notification:nth-last-child(2) {
        transform: scale(0.96) translateY(110%);
        z-index: 1;
    }

    main:not(:hover) div.notification:not(:first-child, :last-child, :nth-last-child(2)) {
        display: none;
    }

    main:not(:hover) .notification:last-child {
        z-index: 2;
    }
</style>