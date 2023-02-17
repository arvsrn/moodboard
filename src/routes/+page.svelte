<script lang="ts">
    import Blanket from "./Blanket.svelte";
    import Card from "./Card.svelte";
    import Main from "./Modal/Main.svelte";
    import Heading from "./Modal/Heading.svelte";
    import MultilineInput from "./MultilineInput.svelte";
    import Navbar from "./Navbar.svelte";
    import Actions from "./Modal/Actions.svelte";
    import Input from "./Input.svelte";

    enum Popup {
        REMOVE_BOARD,
        RENAME_BOARD,
        NONE,
    }

    let showPopup: Popup = Popup.NONE;
    let lists = [
        'Design inspiration',
        'Living room moodboard',
        'Something',
    ];

    let currentList: number = 0;
    let renamePopupInputValue: string = "";
</script>

<Navbar {lists} removeList={i => showPopup = Popup.REMOVE_BOARD} bind:currentList={currentList} renameList={i => showPopup = Popup.RENAME_BOARD}></Navbar>

<main>
    <Card position={[4, 4]} size={["500px", "250px"]}>
        <img src="https://creatorspace.imgix.net/users/cle5e0fjh0000mt0yeh5krcpy/DDN4rzgFJl1zcONw-Fa7OYw0XoAAbrfA.jpeg?w=750&h=750" alt="" draggable="false">
    </Card>

    <Card position={[4, 15]} size={["500px", "fit-content"]}>
        <MultilineInput placeholder="Write something cool here"></MultilineInput>
    </Card>

    <Card position={[25, 4]} size={["500px", "500px"]}>
        
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
{/if}

<svelte:window on:keydown={e => {
    if (e.key === 'Delete') {
        if (lists.length > 1) {
            showPopup = Popup.REMOVE_BOARD;
        }
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
    }
</style>