<script lang="ts">
    export let placeholder: string = "";
</script>

<main contenteditable="true" spellcheck="false" {placeholder}>

</main>

<style>
    main {
        font-family: Inter;
        font-size: 14px;
        line-height: 18px;

        padding: 15px 15px;

        min-height: 48px;
        height: fit-content;

        color: var(--gray12);
        outline: none;
    }

    [placeholder]:empty::before {
        content: attr(placeholder);
        color: var(--gray11); 
        cursor: text;
    }

    [placeholder]:not(:empty)::before {
        content: "";
    }
</style>