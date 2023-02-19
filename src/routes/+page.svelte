<script lang="ts">
    import Blanket from "./Blanket.svelte";
    import Card from "./Card.svelte";
    import Main from "./Modal/Main.svelte";
    import MultilineInput from "./MultilineInput.svelte";
    import Navbar from "./Navbar.svelte";
    import Actions from "./Modal/Actions.svelte";
    import Input from "./Input.svelte";
    import Toast from "./Toast.svelte";
    import TextEmbed from "./Card/TextEmbed.svelte";
    import LinkEmbed from "./Card/LinkEmbed.svelte";

    enum Popup {
        REMOVE_BOARD,
        RENAME_BOARD,
        ADD_ITEM,
        NONE,
    }

    interface Cardd {
        type: 'media' | 'text' | 'link';
        content: string;
        position: [number, number];
        width?: number;
        height?: number;
    }

    let showPopup: Popup = Popup.NONE;
    let lists = [
        'Design inspiration',
        'Living room moodboard',
        'Something',
    ];

    let cards: Array<Cardd> = [
        {
            type: 'text',
            content: '',
            position: [0, 0],
        },
        {
            type: 'link',
            content: 'https://www.youtube.com',
            position: [10, 10],
        }
    ];

    let offset: [number, number] = [200, 200];
    let offsetOffset: [number, number] = [0, 0];
    let dragStart: [number, number] = [0, 0];
    let dragging: boolean = false;

    let currentList: number = 0;
    let renamePopupInputValue: string = "";
    let addToast: (notification: { heading: string; description: string; }) => void;

    let lastScrollTop: number = 0;
    let holdingN: boolean = false;
    let holdingShift: boolean = false;
    let addItemPopupLinkInputValue: string = "";

    async function pasteImage() {
        try {
            const clipboardContents = await navigator.clipboard.read();
            
            for (const item of clipboardContents) {
                if (!item.types.includes("image/png")) {
                    addToast({ heading: 'Error', description: "Clipboard contains non-image data" });
                    return;
                }

                const blob = await item.getType("image/png");
                
                let reader = new FileReader();
                reader.readAsDataURL(blob);
                reader.onloadend = () => {
                    // @ts-ignore
                    const image = new Image();
                    image.src = reader.result?.toString() || "";
                    
                    image.onload = () => {
                        cards = [...cards, {
                            type: 'media',
                            content: reader.result?.toString() || "",
                            position: [0, 0],
                            width: image.width,
                            height: image.height,
                        }];
                        addToast({ heading: 'Added card', description: "Media at [0, 0]" });
                    }
                }
            }
        } catch (error) {
            addToast({ heading: 'Error', description: JSON.stringify(error) });
        }
    }

</script>

<Navbar {lists} removeList={i => {
    if (lists.length > 1) {
        showPopup = Popup.REMOVE_BOARD
    } else {
        addToast({
            heading: 'Can\'t delete',
            description: 'You must have atleast one board.'
        });
    }
}} bind:currentList={currentList} renameList={i => showPopup = Popup.RENAME_BOARD}></Navbar>

<main on:mousedown={e => {
    if (e.button === 1) {
        dragging = true;
        dragStart = [e.clientX, e.clientY];
    };
}} on:touchstart|self={e => {
    console.log('Uranium-235');

    dragging = true;
    dragStart = [
        e.changedTouches[0].pageX,
        e.changedTouches[0].pageY,
    ];
}} on:paste|preventDefault={async e => {
    if (!e.clipboardData) {
        addToast({ heading: 'Error', description: 'clipboardData is null' });
        return;
    }
    
    pasteImage();
}}>
    {#each cards as card} 
        {#if card.type === 'text'}
            <TextEmbed bind:position={card.position} bind:offset={offset}></TextEmbed>
        {:else if card.type === 'link'}
            <LinkEmbed bind:position={card.position} bind:offset={offset} link={card.content}></LinkEmbed>
        {:else if card.type === 'media'}
            <!--Only supports images for now-->
            <Card bind:position={card.position} size={[
                card.width ? card.width - (card.width % 25) + "px" : "0px", 
                card.height ? card.height - (card.height % 25) + "px" : "0px"
            ]} bind:offset={offset}>
                <img src={card.content} alt="" draggable="false">
            </Card>
        {/if}
    {/each}
</main>

{#if showPopup === Popup.REMOVE_BOARD}
<Blanket onClick={() => showPopup = Popup.NONE}>
    <Main>
        <div style="display:flex;flex-direction:column;align-items:flex-start;padding:24px;gap:16px;border-bottom:1px solid #232323;">
            <h1 style="font-family:Inter;font-style:normal;font-weight:700;font-size:14px;line-height:17px;color:var(--gray12);">
                Remove '{lists[currentList]}'
            </h1>
            <p style="font-family:Inter;font-style:normal;font-weight:400;font-size:14px;line-height:17px;color:#A0A0A0;">Are you sure? This cannot be undone.</p>
        </div>
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
        <div style="display:flex;flex-direction:column;align-items:flex-start;padding:24px;gap:16px;border-bottom:1px solid #232323;">
            <h1 style="font-family:Inter;font-style:normal;font-weight:700;font-size:14px;line-height:17px;color:var(--gray12);">
                Rename board
            </h1>
            <Input {addToast} bind:value={renamePopupInputValue} placeholder={lists[currentList]}></Input>
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
        <div style="display:flex;flex-direction:column;align-items:flex-start;padding:24px;gap:16px;width:100%;height:fit-content;">
            <h1 style="font-family:Inter;font-style:normal;font-weight:700;font-size:14px;line-height:17px;color:var(--gray12);">
                Add card
            </h1>
            <Input {addToast} regex={/[-a-zA-Z0-9@:%._\+~#=]{1,256}\.[a-zA-Z0-9()]{1,6}\b([-a-zA-Z0-9()@:%_\+.~#?&//=]*)/} errorMessage="Input must be link" autofocus bind:value={addItemPopupLinkInputValue} placeholder="Paste link" onEnter={() => {
                // Add link embed
                cards = [...cards, {
                    type: 'link',
                    content: addItemPopupLinkInputValue,
                    position: [0, 0]
                }];
                showPopup = Popup.NONE;
                addToast({
                    heading: 'Added card',
                    description: 'Link embed at [0, 0]'
                });
            }}></Input>
            <div style="display:flex;flex-direction:row;align-items:flex-start;padding:0px;gap:16px;">
                <button class="card-option">
                    <img draggable="false" src="https://cdn.discordapp.com/attachments/1074712152771919934/1076533443715940502/image.png" alt="">
                    <p style="font-family:Inter;font-style:normal;font-weight:700;font-size:14px;line-height:16px;color:var(--gray12);position:absolute;left:12px;bottom:12px;">Media</p>
                </button>
                <button class="card-option" on:click={() => {
                    // Add text block
                    cards = [...cards, {
                        type: 'text',
                        position: [0, 0],
                        content: ''
                    }];
                    showPopup = Popup.NONE;
                    addToast({
                        heading: 'Added card',
                        description: 'Text at [0, 0]'
                    });
                }}>
                    <img draggable="false" src="https://cdn.discordapp.com/attachments/1074712152771919934/1076533394126680064/image.png" alt="">
                    <p style="font-family:Inter;font-style:normal;font-weight:700;font-size:14px;line-height:16px;color:var(--gray1);position:absolute;left:12px;bottom:12px;">Text</p>
                </button>
            </div>
        </div>
    </Main>
</Blanket>
{/if}

<!--WIP-->
<Toast bind:addNotification={addToast}></Toast>

<button class="tip" on:click={() => showPopup = Popup.ADD_ITEM}>
    Add card 
    <svg style="margin-left:4px;" width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg" class:active={holdingShift}>
        <rect width="20" height="20" rx="4" fill="var(--bg)"/>
        <path d="M3.81818 11.2273L9.95455 5.09091L16.0909 11.2273H13.0909V14.5H6.81818V11.2273H3.81818ZM7.25284 9.94886H8.59091V13.2216H11.3182V9.94886H12.6562L9.95455 7.24716L7.25284 9.94886Z" fill="var(--fg)"/>
    </svg>           
    <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg" class:active={holdingN}>
        <rect width="20" height="20" rx="4" fill="var(--bg)"/>
        <path d="M13.6136 5.77273V14.5H11.6364L8.48295 9.91477H8.43182V14.5H6.0625V5.77273H8.07386L11.1761 10.3409H11.2443V5.77273H13.6136Z" fill="var(--fg)"/>
    </svg>           
</button>

<svelte:window on:keydown={e => {
    console.log(e);
    
    if (e.key === 'Delete') {
        if (lists.length > 1) {
            showPopup = Popup.REMOVE_BOARD;
        } else {
            addToast({
                heading: 'Can\'t delete',
                description: 'You must have atleast one board.'
            });
        }
    } else if ((e.key === 'N' || e.key === 'n') && e.shiftKey) {
        showPopup = Popup.ADD_ITEM;
    } 
    
    if (e.key === 'N' || e.key === 'n') {
        holdingN = true;
    } else if (e.key === 'Shift') {
        holdingShift = true;
    }
}} on:keyup={e => {
    if (e.key === 'N' || e.key === 'n') {
        holdingN = false;
    } else if (e.key === 'Shift') {
        holdingShift = false;
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
}} on:touchend={() => {
    dragging = false;
    offsetOffset = [0, 0];
}} on:touchmove={e => {
    if (dragging) {
        offset[0] -= offsetOffset[0];
        offset[1] -= offsetOffset[1];
        
        offsetOffset = [
            e.changedTouches[0].pageX - dragStart[0], 
            e.changedTouches[0].pageY - dragStart[1]
        ];

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

        overflow: hidden;
    }

    img {
        width: 100%;
        user-select: none;
    }

    button.card-option {
        width: 100%;
        aspect-ratio: 1/1;

        position: relative;

        border-radius: 12px;
        outline: none;
        overflow: hidden;
        border: none;
        cursor: pointer;
    }

    button.card-option > img {
        transition: transform 0.1s ease-in-out;
    }

    button.card-option:hover > img {
        transform: scale(1.1);
    }

    button.tip {
        font-family: Inter;
        font-size: 13px;
        font-weight: 600;
        color: var(--gray11);
        
        position: absolute;
        left: 50%;
        bottom: 24px;
        transform: translateX(-50%);

        padding: 8px 12px;

        background: transparent;
        border: none;
        outline: none;
        border-radius: 6px;

        transition: background 0.1s ease-in-out;

        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
        gap: 2px;
    }

    button.tip:hover {
        background: var(--gray4);
    }

    svg {
        --bg: #282828;
        --fg: #7E7E7E;
    }

    svg.active {
        --bg: #343434;
        --fg: #A0A0A0;
    }
</style>