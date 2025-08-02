<script>
  import DocumentDetails from './DocumentDetails.svelte';
  let isOpen = false;
</script>

<style>
  .folder {
    border: 1px solid #444;
    background-color: #eee;
    padding: 0.75rem;
    cursor: pointer;
  }

  .document-container {
    margin-top: 0.5rem;
    padding-left: 1rem;
  }
</style>

<div class="folder" on:click={() => isOpen = !isOpen}>
  📁 Memorandum
</div>

{#if isOpen}
  <div class="document-container">
    <DocumentDetails />
  </div>
{/if}
