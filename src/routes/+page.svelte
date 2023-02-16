<script lang="ts">
    import Card from "./Card.svelte";
    import MultilineInput from "./MultilineInput.svelte";
</script>

<main>
    <Card position={[4, 4]} size={["500px", "250px"]}>
        <img src="https://creatorspace.imgix.net/users/cle5e0fjh0000mt0yeh5krcpy/DDN4rzgFJl1zcONw-Fa7OYw0XoAAbrfA.jpeg?w=750&h=750" alt="" draggable="false">
    </Card>

    <Card position={[4, 15]} size={["500px", "fit-content"]}>
        <MultilineInput placeholder="Write something cool here"></MultilineInput>
    </Card>

    <Card position={[25, 4]} size={["500px", "500px"]} style="twitter">
        
    </Card>
</main>

<style>
    main {
        width: 100vw;
        height: 100vh;

        background-color: #F3F3F3;
        position: absolute;

        overflow: scroll;
    }

    img {
        width: 100%;
        user-select: none;
    }
</style>