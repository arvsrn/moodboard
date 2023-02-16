<script lang="ts">
    import { CaretRight } from "radix-icons-svelte";

    export let icon: ConstructorOfATypedSvelteComponent | undefined = undefined;
    export let text: string;
    export let key: string = "";
    export let action: () => void;

    let showSubmenu: boolean = false;
</script>

<button on:click={action} on:mouseenter={() => showSubmenu = true} on:mouseleave={() => showSubmenu = false}>
    {#if icon}
        <svelte:component this={icon}></svelte:component>
    {/if}
    {text} <span>{key} {#if $$slots.submenu} <CaretRight></CaretRight> {/if}</span>

    {#if showSubmenu && $$slots.submenu}
        <div on:mouseenter={() => showSubmenu = true} on:mouseleave={() => showSubmenu = false}><slot name="submenu"/></div>
    {/if}
</button>

<style>
    div {
        width: fit-content;
        height: fit-content;
        background: transparent;

        position: absolute;
        top: -6px;
        left: 101%;
    }

    button {
        width: 100%;
        height: 32px;
        
        font-family: 'Inter';
        font-weight: 500;
        font-size: 13px;
        line-height: 15px;

        background: transparent;        
        color: #222222;
        border-radius: 4px;

        display: flex;
        flex-direction: row;
        align-items: center;
        padding: 2px 10px;
        gap: 8px;
        
        outline: none;
        border: none;
        cursor: pointer;

        position: relative;
    }

    button:hover {
        background: #F3F3F3;
    }

    span {
        font-family: Inter;
        font-size: 12px;
        
        color: #A0A0A0;
        margin-left: auto;
    }
</style>