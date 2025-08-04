<script>
  import Drawer from "./Drawer.svelte";
  import { mockData } from "$lib/mock/data.js";
</script>

<div class="cabinet">
  {#each mockData as item, index}
    <Drawer category={item.category} documents={item.documents} />
  {/each}
</div>

<style>
  .cabinet {
    background-color: #202020;
    width: 250px;
    height: 90%;
    padding: 10px;
    margin: 3rem 2rem;
    border-radius: 3px;
  }

  @media (max-width: 900px) {
    .cabinet {
      width: 100%;
    }
  }
</style>
