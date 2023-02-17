<script lang="ts">
    import Blanket from "./Blanket.svelte";
    import Card from "./Card.svelte";
    import Main from "./Modal/Main.svelte";
    import Heading from "./Modal/Heading.svelte";
    import MultilineInput from "./MultilineInput.svelte";
    import Navbar from "./Navbar.svelte";
    import Actions from "./Modal/Actions.svelte";
    import Input from "./Input.svelte";
    import Notifications from "./Notifications.svelte";
    import { Image, Text } from "radix-icons-svelte";

    enum Popup {
        REMOVE_BOARD,
        RENAME_BOARD,
        ADD_ITEM,
        NONE,
    }

    let showPopup: Popup = Popup.NONE;
    let lists = [
        'Design inspiration',
        'Living room moodboard',
        'Something',
    ];

    let offset: [number, number] = [0, 0];
    let offsetOffset: [number, number] = [0, 0];
    let dragStart: [number, number] = [0, 0];
    let dragging: boolean = false;

    let currentList: number = 0;
    let renamePopupInputValue: string = "";
    let notifications: Array<string> = [];
</script>

<Navbar {lists} removeList={i => showPopup = Popup.REMOVE_BOARD} bind:currentList={currentList} renameList={i => showPopup = Popup.RENAME_BOARD}></Navbar>

<main on:mousedown={e => {
    if (e.button === 1) {
        dragging = true;
        dragStart = [e.clientX, e.clientY];
    };
}}>
    <Card position={[4, 4]} size={["500px", "250px"]} bind:offset={offset}>
        <img src="https://creatorspace.imgix.net/users/cle5e0fjh0000mt0yeh5krcpy/DDN4rzgFJl1zcONw-Fa7OYw0XoAAbrfA.jpeg?w=750&h=750" alt="" draggable="false">
    </Card>

    <Card position={[4, 15]} size={["500px", "fit-content"]} bind:offset={offset}>
        <MultilineInput placeholder="Write something cool here"></MultilineInput>
    </Card>

    <Card position={[25, 4]} size={["200px", "200px"]} bind:offset={offset}>
        
    </Card>
</main>

{#if showPopup === Popup.REMOVE_BOARD}
<Blanket onClick={() => showPopup = Popup.NONE}>
    <Main>
        <Heading title="Remove board '{lists[currentList]}'" description="Are you sure? This cannot be undone."></Heading>
        <Actions primaryButtonCallback={() => {
            lists.splice(currentList, 1);
            lists = lists;
            showPopup = Popup.NONE;
        }} secondaryButtonCallback={() => showPopup = Popup.NONE} style="danger" secondaryButtonLabel="Cancel" primaryButtonLabel="Remove"></Actions>
    </Main>
</Blanket>
{:else if showPopup === Popup.RENAME_BOARD}
<Blanket onClick={() => showPopup = Popup.NONE}>
    <Main>
        <Heading title="Rename board" description=""></Heading>
        <div style="width:100%;height:fit-content;padding:0px 16px 16px 24px;">
            <Input placeholder={lists[currentList]} bind:value={renamePopupInputValue}/>
        </div>
        <Actions primaryButtonCallback={() => {
            lists[currentList] = renamePopupInputValue;
            showPopup = Popup.NONE;
        }} secondaryButtonCallback={() => showPopup = Popup.NONE} style="normal" secondaryButtonLabel="Cancel" primaryButtonLabel="Save"></Actions>
    </Main>
</Blanket>
{:else if showPopup === Popup.ADD_ITEM}
<Blanket onClick={() => showPopup = Popup.NONE}>
    <Main>
        <Heading title="Paste link" description="Paste any link and it'll be embedded appropriately."></Heading>
        <div style="width:100%;height:fit-content;padding:0px 12px 0px 12px;">
            <Input value="" placeholder="Link here..."></Input>
        </div>
        <Heading title="Other widgets" description=""></Heading>
        <div style="width:100%;height:fit-content;padding:0px 12px;display:flex;flex-direction:column;gap:6px;padding-bottom:4px;">
            <button><Image/> Pictures & Video</button>
            <button><Text/> Note</button>
        </div>
    </Main>
</Blanket>
{/if}

<!--WIP-->
<Notifications bind:notifications={notifications}></Notifications>

<svelte:window on:keydown={e => {
    if (e.key === 'Delete') {
        if (lists.length > 1) {
            showPopup = Popup.REMOVE_BOARD;
        }
    }
}} on:mouseup={() => {
    dragging = false;
    offsetOffset = [0, 0];
}} on:mousemove={e => {
    if (dragging) {
        offset[0] -= offsetOffset[0];
        offset[1] -= offsetOffset[1];
        
        offsetOffset = [e.clientX - dragStart[0], e.clientY - dragStart[1]];

        offset[0] += offsetOffset[0];
        offset[1] += offsetOffset[1];
    }
}}></svelte:window>

<style>
    main {
        width: 100vw;
        height: 100vh;

        background-color: var(--gray2);
        position: absolute;

        overflow: auto;
    }

    img {
        width: 100%;
        user-select: none;
        filter: saturate(50%);
    }

    button {
        width: 100%;
        height: 36px;

        background-color: var(--gray2);
        border: 1px solid var(--gray4);

        outline: none;

        color: var(--gray12);

        border-radius: 8px;
        transition: transform 0.1s ease-in-out;

        overflow: hidden;
        cursor: pointer;

        position: relative;

        font-size: 14px;
        font-family: Inter;
        font-weight: 500;

        display: flex;
        flex-direction: row;
        gap: 8px;
        align-items: center;
        padding: 12px;
    }

    button:hover {
        transform: scale(1.01);
    }

    button:active {
        transform: scale(0.99);
    }
</style>