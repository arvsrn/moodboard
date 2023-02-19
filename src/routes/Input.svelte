<script lang="ts">
    import { onMount } from "svelte";

    export let placeholder: string = "";
    export let value: string;
    export let disabled: boolean = false;
    export let onEnter: () => void = () => {};
    export let autofocus: boolean = false;
    export let regex: RegExp = /.*/;
    export let errorMessage: string = "";
    export let addToast: (notification: { heading: string, description: string }) => void;

    let self: HTMLInputElement;

    onMount(() => {
        if (autofocus) self.focus();
    });
</script>

<input bind:this={self} type="text" {placeholder} bind:value={value} {disabled} class:error={!regex.test(value)} on:keypress={e => {
    if (e.key === 'Enter') {
        if (regex.test(value)) {
            onEnter();
        } else {
            addToast({ heading: 'Invalid input', description: errorMessage });
        }
    }
}}>

<style>
    input {
        width: 100%;
        height: 36px;

        background-color: var(--gray1);
        border: 1px solid var(--gray3);
        color: var(--gray12);
        border-radius: 8px;

        padding-left: 12px;

        outline: none;
    }

    input::placeholder {
        color: var(--gray11);
    }

    input.error {
        border: 1px solid red;
    }
</style>