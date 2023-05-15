<script>
    export let showmodal = false;

</script>
{#if showmodal}
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <div class="backdrop" on:click|self>
        <div class="modal">
            <h3>Add Associates</h3>
            <slot></slot>
        </div>
    </div>
{/if}
<style>
.backdrop {
    background: rgba(0, 0, 0, 0.8);
    width: 100%;
    height: 100%;
    position: fixed;
    margin: 0;
}
.modal {
    background: white;
    max-width: 400px;
    margin: 200px auto;
    padding: 10px;
    text-align: center;
    border-radius: 10px;
}
</style>