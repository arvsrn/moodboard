<script lang="ts">
    import { onMount } from "svelte";
    import Card from "../Card.svelte";

    export let offset: [number, number];
    export let position: [number, number];
    export let link: string;

    onMount(() => {
        fetch(link, { method: 'GET' }).then(res => {
            console.log(res.body);
        });
    });
</script>

<Card bind:position={position} size={["300px", "175px"]} bind:offset={offset}>
    <div style="padding:24px;width:100%;height:100%;display:flex;flex-direction:column;gap:6px;">
        <div style="width:40px;height:40px;border-radius:12px;border:1px solid var(--gray6);margin-bottom:8px;display:flex;align-items:center;justify-content:center;">
            <img style="width:20px;height:16px;" src="" alt="">
        </div>
        <p style="font-family:Inter;font-size:14px;font-weight:600;color:var(--gray12);width:100%;word-wrap:break-word;">{link}</p>
        <p style="font-family:Inter;font-size:12px;color:var(--gray11);">{link}</p>
    </div>
</Card>