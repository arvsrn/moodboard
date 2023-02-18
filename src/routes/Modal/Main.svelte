<main>
    <slot></slot>
</main>

<style>
    main {
        width: 400px;
        min-height: 64px;
        height: fit-content;

        border-radius: 12px;
        background-color: var(--gray1);
        border: 1px solid var(--gray2);

        position: relative;
        overflow: hidden;
    }
</style>