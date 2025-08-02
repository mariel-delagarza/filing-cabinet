<script>
  import Folder from './Folder.svelte';
  export let data;

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
    transition: background-color 0.3s ease;
  }

  .drawer:hover {
    background-color: #bbb;
  }

  .folder-container {
    margin-top: 1rem;
    padding-left: 1rem;
  }
</style>

<div class="drawer" on:click={() => isOpen = !isOpen}>
  <strong>{data.category}</strong>
</div>

{#if isOpen}
  <div class="folder-container">
    <Folder type={data.resource_type} documents={data.documents} />
  </div>
{/if}
