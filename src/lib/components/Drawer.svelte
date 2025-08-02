<script>
  import Folder from './Folder.svelte';
  export let data;

  let isOpen = false;
</script>

<div class="cabinet">
  <!-- Top (Active) Drawer -->
  <div class="drawer" on:click={() => isOpen = !isOpen}>
    <strong>{data.category}</strong>
    <div class="handle"></div>
  </div>

  {#if isOpen}
    <div class="folder-container">
      <Folder type={data.resource_type} documents={data.documents} />
    </div>
  {/if}

  <!-- Bottom (Placeholder) Drawer -->
  <div class="bottom-drawer">
    <em>Drawer 2 (coming soon)</em>
  </div>
</div>


<style>
  .cabinet {
    background: #d9d9d9;
    border: 4px solid #333;
    border-radius: 6px;
    width: 320px;
    padding: 1rem;
    box-shadow: inset 0 0 0 2px #999;
  }

  .drawer {
    background: #ccc;
    border: 2px solid #444;
    padding: 1rem;
    margin-bottom: 1rem;
    cursor: pointer;
    position: relative;
    display: flex;
    justify-content: space-between;
    align-items: center;
    transition: background 0.3s;
  }

  .drawer:hover {
    background: #bbb;
  }

  .handle {
    width: 32px;
    height: 16px;
    background: #aaa;
    border: 2px solid #222;
    border-radius: 2px;
  }

  .folder-container {
    margin-top: 0.75rem;
    padding-left: 1rem;
  }

  .bottom-drawer {
    background: #b4b4b4;
    border: 2px solid #444;
    padding: 1rem;
    opacity: 0.6;
  }
</style>
