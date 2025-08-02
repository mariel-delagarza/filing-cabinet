<script>
  import DocumentDetails from './DocumentDetails.svelte';
  export let type;
  export let documents = [];

  let isOpen = false;
</script>

<style>
  .folder {
    border: 1px solid #444;
    background-color: #eee;
    padding: 0.75rem;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .folder:hover {
    background-color: #ddd;
  }

  .document-container {
    margin-top: 0.5rem;
    padding-left: 1rem;
  }
</style>

<div class="folder" on:click={() => isOpen = !isOpen}>
  📁 {type}
</div>

{#if isOpen}
  <div class="document-container">
    {#each documents as doc}
      <DocumentDetails doc={doc} />
    {/each}
  </div>
{/if}
