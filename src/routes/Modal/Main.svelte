<main>
    <div class="glow" style='left:5px;top:25%;'></div>
    <div class="glow" style='left:90px;top:25%;'></div>
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
        padding: 8px 0px;

        position: relative;
        overflow: hidden;
    }

    div.glow {
        position: absolute;
        
        width: 186.5px;
        height: 30.02px;

        background: linear-gradient(181.14deg, rgba(255, 255, 255, 0) 0.92%, rgba(155, 155, 155, 0.13) 49.98%, rgba(255, 255, 255, 0) 99.03%);
        filter: blur(20px);
        transform: rotate(-70.27deg);
        
        pointer-events: none;
    }
</style>