<!-- src/PostIt.svelte -->
<script>
  export let text = "";
  export let startDate;
  export let endDate;
  export let tags = [];

  $: if (tags.length) {
    console.log("Tags:", tags);
  }

</script>

<div class="post-it">
  <p class="text">{text}</p>
  {#if startDate}
    <p class="text">Oldest Date:<br> {startDate}</p>
  {/if}
  {#if endDate}
    <p class="text">Latest Date:<br> {endDate}</p>
  {/if}
  {#if (tags.length)}
    {#each tags as tag}
      <p class="tag">{tag},</p>
    {/each}
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
    font-family: "Rock Salt", cursive;
    transform: rotate(2deg);
    position: relative;
    z-index: 4;
  }

  .text {
    max-width: 80%;
    margin: 2rem auto 0 auto;
    font-size: 1rem;
    line-height: 1.5;
    transform: rotate(2deg);
  }

  .tag {
    max-width: 80%;
    margin: 0 auto;
    font-size: 1rem;
    line-height: 1.5;
    transform: rotate(2deg);
  }
</style>
