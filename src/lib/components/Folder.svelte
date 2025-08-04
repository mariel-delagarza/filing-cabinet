<script>
  export let phases = []; // an array of labels
</script>

<div class="folder">
  <div class="body">
    <!-- This is the visible open folder -->
  </div>

  <!-- Stack of tabs poking out from the right side -->
  {#each phases as label, i}
    <div class="tab" style="top: {`${i * 3}rem`}">
      {label}
    </div>
  {/each}
</div>

<style>
  .folder {
    position: relative;
    width: 30rem;
    height: 100%;
    background-image: url("/src/assets/light_wood.jpeg");
    background-size: cover;
    background-position: center;
    background-color: beige;
    border: 1px solid #999;
    margin-bottom: 2rem;
  }

  /* Folder body */
  .body {
    width: 100%;
    height: 100%;
  }

  /* Folder tabs stacked on the right */
  .tab {
    position: absolute;
    right: -3rem;
    width: 2.5rem;
    writing-mode: vertical-rl;
    transform: rotate(180deg);
    background: #fdfadd;
    border: 2px solid #ccc;
    border-right: 6px solid #aaa;
    border-radius: 0 0.5rem 0.5rem 0;
    padding: 1rem 0.5rem;
    font-size: 0.75rem;
    font-weight: bold;
    box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.1);
    z-index: 2;
    cursor: pointer;
  }
</style>
