<script lang="ts">
    import Monaco from "$lib/Monaco.svelte";
    import Main from "$lib/Main.java?raw"
</script>

<Monaco value={Main} language={"java"}/>

<style global>
    :global(body, html) {
        padding: 0;
        margin: 0;
        width: 100%;
        height: 100%;
    }
</style>