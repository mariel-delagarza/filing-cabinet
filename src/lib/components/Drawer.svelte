<script>
  import Folder from './Folder.svelte';

  let isOpen = false;
</script>

<style>
  .drawer {
    border: 2px solid #333;
    background-color: #ccc;
    width: 300px;
    padding: 1rem;
    cursor: pointer;
    margin-bottom: 1rem;
  }

  .folder-container {
    margin-top: 1rem;
    padding-left: 1rem;
  }
</style>

<div class="drawer" on:click={() => isOpen = !isOpen}>
  <strong>Category A</strong>
</div>

{#if isOpen}
  <div class="folder-container">
    <Folder />
  </div>
{/if}
