<script lang="ts">
    import { Sun, Moon, Pencil2, Link1 } from 'radix-icons-svelte';
    import { onMount } from 'svelte';
    import ContextMenu from './ContextMenu/Main.svelte';
    import Option from './ContextMenu/Option.svelte';

    // is light mode
    let mode: boolean = false;
    let mounted: boolean = false;
    let showLists: boolean = false;

    export let removeList: (i: number) => void;
    export let renameList: (i: number) => void;
    export let lists: Array<string>;
    export let currentList: number = 0;

    onMount(() => mounted = true);

    const onModeChange = () => {
        if (!mounted) return;

        if (mode) {
            document.body.className = 'light';
        } else {
            document.body.className = 'dark';
        }
    };

    $: mode, onModeChange();
</script>

<nav>
    <button class="square" style="color: var(--gray12);">
        <svg width="19" height="21" viewBox="0 0 19 21" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M0.888889 16.5378L8.61111 12.0757V21H10.3889V12.0757L18.1111 16.5378L19 14.9761L11.3056 10.5139L19 6.05179L18.1111 4.49004L10.3889 8.95219V0H8.61111V8.95219L0.888889 4.49004L0 6.05179L7.69444 10.5139L0 14.9761L0.888889 16.5378Z" fill="currentColor"/>
        </svg>                  
    </button>
    <div style="position: relative">
        <button class="list" on:click={() => showLists = true}>
            {lists[currentList]}
            <svg width="7" height="10" viewBox="0 0 7 10" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" clip-rule="evenodd" d="M0.10518 3.90805C0.252079 4.07951 0.498184 4.08819 0.654867 3.92746L3.50001 1.00882L4.92256 2.46814L6.34512 3.92746C6.50184 4.08819 6.74793 4.07951 6.89485 3.90805C7.0417 3.7366 7.03377 3.4673 6.87712 3.30657L3.76598 0.115091C3.61639 -0.0383637 3.38362 -0.0383637 3.23403 0.115091L0.122914 3.30657C-0.0337778 3.4673 -0.0417111 3.7366 0.10518 3.90805Z" fill="currentColor"/>
                <path fill-rule="evenodd" clip-rule="evenodd" d="M0.10518 6.09153C0.252079 5.92007 0.498184 5.91139 0.654867 6.07212L3.50001 8.99076L6.34512 6.07212C6.50184 5.91139 6.74793 5.92007 6.89485 6.09153C7.0417 6.26298 7.03377 6.53227 6.87712 6.69301L3.76598 9.88451C3.61639 10.038 3.38362 10.038 3.23403 9.88451L0.122914 6.69301C-0.0337778 6.53227 -0.0417111 6.26298 0.10518 6.09153Z" fill="currentColor"/>
            </svg>
        </button>

        {#if showLists}
            <ContextMenu bind:showContextMenu={showLists} contextMenuPosition={[0, 40]}>
                {#each lists as list, i}
                    <Option text={list} action={() => {
                        currentList = i;
                        showLists = false;
                    }}></Option>
                {/each}

                <div style="width:100%;height:1px;background:var(--gray3);margin:6px 0px;"></div>
                <Option text="Rename" action={() => renameList(currentList)} icon={Pencil2}></Option>
                <Option text="Remove" action={() => removeList(currentList)} key="Del"></Option>
            </ContextMenu>
        {/if}
    </div>
    <div style="margin-left:auto;display:flex;flex-direction:row;gap:8px;align-items:center;">
        <button class="list">
            <Link1 /> Copy link
        </button>
        <button class="square" on:click={() => mode = !mode}>
            {#if mode}
                <Moon></Moon>
            {:else}
                <Sun></Sun>
            {/if}
        </button>
    </div>
</nav>

<style>
    button.square {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;

        color: var(--gray11);
        
        width: 40px;
        height: 40px;

        background-color: var(--gray2);
        border: 1px solid var(--gray5);
        outline: none;
        border-radius: 12px;
        
        cursor: pointer;
        transition: transform 0.1s ease-in-out;
    }

    button.square:hover {
        transform: scale(1.05);
    }

    button.square:active {
        transform: scale(0.95);
    }

    button.list {
        width: fit-content;
        height: 36px;

        border-radius: 8px;
        color: var(--gray12);

        font-size: 14px;
        font-weight: 500;
        line-height: 15px;
        padding: 10.5px;

        outline: none;
        cursor: pointer;
        background-color: transparent;
        border: none;

        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: flex-start;
        gap: 6px;

        transition: background-color 0.1s ease-in-out, transform 0.1s ease-in-out;
    }

    button.list:hover {
        background-color: var(--gray4);
    }

    button.list:active {
        transform: scale(0.95);
    }

    nav {
        position: absolute;
        top: 0px;
        left: 0px;
        z-index: 1000;
        
        width: 100vw;
        height: 100px;

        gap: 8px;

        display: flex;
        flex-direction: row;
        align-items: center;
        padding: 30px;

        background: rgba(255, 255, 255, 0.001);
        backdrop-filter: blur(27.5px);
    }
</style>