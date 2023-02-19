<script lang="ts">
    import Card from "../Card.svelte";
    import MultilineInput from "../MultilineInput.svelte";

    export let offset: [number, number];
    export let position: [number, number];
</script>

<Card bind:position={position} size={["500px", "fit-content"]} bind:offset={offset}>
    <MultilineInput placeholder="Write something cool here"></MultilineInput>
</Card>