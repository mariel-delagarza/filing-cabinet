<script>
  import Cabinet from "./Cabinet.svelte";
  import Folder from "./Folder.svelte";


  let folders = [
    { id: 1, label: "Pre-Negotiation" },
    { id: 2, label: "Negotiation" },
    { id: 3, label: "Implementation" },
    { id: 4, label: "Dispute Resolution" }
  ];

  let activeId = null;
</script>

<div class="wrapper">
  <h1>Filing Cabinet MVP</h1>

  <div class="main">
    <Cabinet />
    <div class="folder-area">
      {#each folders as folder}
        <Folder
          label={folder.label}
          isOpen={folder.id === activeId}
          on:click={() => (activeId = folder.id)}
        />
      {/each}
    </div>
  </div>
</div>

<style>
  :global(body) {
    margin: 0;
    overflow: hidden;
    background: #d2d0d0;
  }

  h1 {
    height: 60px;
    margin: 0;
    padding: 1rem;
    flex-shrink: 0;
  }
  .wrapper {
    /* max-width: 1900px; */
    height: 100vh;
    /* margin: 0 auto; */
    padding: 1rem;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
  }

  .main {
    flex: 1;
    display: flex;
    overflow: hidden;
    gap: 2rem;
  }

  .folder-area {
    background-image: url("../assets/dark_wood.jpeg");
    background-size: cover;
    background-position: center;
    flex: 1;
    overflow-y: auto;
    padding: 1rem;
    box-sizing: border-box;
  }

  @media (max-width: 900px) {
    .main {
      flex-direction: column;
    }

    .folder-area {
      width: 100%;
    }
  }
</style>
