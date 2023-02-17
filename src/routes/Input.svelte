<script lang="ts">
    export let placeholder: string = "";
    export let value: string;
</script>

<input type="text" {placeholder} bind:value={value}>

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
</style>