<!-- src/PostIt.svelte -->
<script>
  export let text = "Write something here!";
  export let startDate;
  export let endDate;
</script>

<div class="post-it">
  <p>{text}</p>
  {#if startDate}
    <p>Oldest Date:<br> {startDate}</p>
  {/if}
  {#if endDate}
    <p>Latest Date:<br> {endDate}</p>
  {/if}
</div>

<style>
  .post-it {
    background-image: url("../assets/old-note.png");
    background-size: cover;
    background-position: center;
    width: 350px;
    min-height: 250px;
    padding: 1.25rem;
    /* box-shadow: 3px 3px 6px rgba(0, 0, 0, 0.2); */
    font-family: "Rock Salt", cursive;
    transform: rotate(2deg);
    position: relative;
    z-index: 4;
    /* box-shadow:
      inset 0 -40px 40px rgba(0, 0, 0, 0.1),
      inset 0 25px 10px rgba(0, 0, 0, 0.1),
      0 5px 6px 5px rgba(0, 0, 0, 0.1); */
  }

  .post-it p {
    max-width: 80%;
    margin: 2rem auto 0 auto;
    font-size: 1rem;
    line-height: 2.5;
    transform: rotate(2deg);
  }
</style>
