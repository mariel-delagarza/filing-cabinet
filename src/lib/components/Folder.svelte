<script lang="ts">
  let folders = [
    { id: 1, label: "Pre-Negotiation" },
    { id: 2, label: "Negotiation" },
    { id: 3, label: "Implementation" },
    { id: 4, label: "Dispute Resolution" }
  ];

  function handleClick(folderId: number) {
    console.log("Clicked folder", folderId);
    // later: emit event or update store to slide + open folder
  }
</script>

<div class="folders">
  {#each folders as folder}
    <div class="folder-tab" on:click={() => handleClick(folder.id)}>
      {folder.label}
    </div>
  {/each}
</div>

<style>
  .folders {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    padding: 1rem;
  }

  .folder-tab {
    writing-mode: vertical-rl;
    transform: rotate(180deg); /* makes text upright in vertical-rl mode */
    background: beige;
    border: 1px solid black;
    border-radius: 0.75rem 0 0 0.75rem;
    padding: 0.5rem 0.75rem;
    font-size: 0.8rem;
    cursor: pointer;
    box-shadow: 2px 2px 5px rgba(0,0,0,0.1);
    transition: background 0.2s;
  }

  .folder-tab:hover {
    background: #eee;
  }
</style>
