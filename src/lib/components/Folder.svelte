<script>
  export let phases = []; // an array of strings
</script>

<div class="folder">
  <div class="tab-bar">
    {#each phases as label}
      <div class="tab">
        {label}
      </div>
    {/each}
  </div>

  <div class="body">
    <!-- folder content goes here -->
  </div>
</div>

<style>
  .folder {
    position: relative;
    width: 40%;
    height: 100%;
    background: linear-gradient(to left, #fdfadd 80%, #cfc7a0 100%);
    z-index: 2;
  }

  /* Tab bar with horizontal tabs */
  .tab-bar {
    position: absolute;
    right: -2.1rem; /* offset to the right of folder */
    top: 0;
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }

  /* Individual tabs */
  .tab {
    writing-mode: vertical-rl;
    background: #fdfadd;
    border-radius: 0 0.5rem 0.5rem 0;
    padding: 1rem 0.5rem;
    font-size: 1rem;
    font-weight: bold;
    cursor: pointer;
    text-align: center;
  }

  /* Apply shadow to all tabs except the first one */
  .tab:not(:first-child) {
    background: linear-gradient(to left, #fdfadd 80%, #cfc7a0 100%);
  }
</style>
