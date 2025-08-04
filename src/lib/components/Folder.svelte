<script>
  export let phases = []; // an array of labels
</script>

<div class="folder">
  <div class="body">
    <!-- This is the visible open folder -->
  </div>

  <!-- Stack of tabs poking out from the right side -->
  {#each phases as label, i}
    <div class="tab" style="top: {`${i * 9}rem`}">
      {label}
    </div>
  {/each}
</div>

<style>
  .folder {
    position: relative;
    width: 45%;
    height: 100%;
    background-image: url("/src/assets/light_wood.jpeg");
    background-size: cover;
    background-position: center;
    background-color: beige;
    margin-bottom: 2rem;
    z-index: 2;
  }

  /* Folder body */
  .body {
    width: 100%;
    height: 100%;
  }

  /* Folder tabs stacked on the right */
  .tab {
    position: absolute;
    right: -2.5rem;
    width: 1.5rem;
    writing-mode: vertical-rl;
    background: #fdfadd;
    outline: 0.5px solid #ccc;
    border-radius: 0 0.5rem 0.5rem 0;
    padding: 1rem 0.5rem;
    font-size: 1rem;
    font-weight: bold;
    box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.6);
    z-index: 0;
    cursor: pointer;
  }
</style>
