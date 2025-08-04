<script>
  import Drawer from "./Drawer.svelte";
  import { mockData } from "$lib/mock/data.js";
  import { createEventDispatcher } from "svelte";

  export let activeDrawer;
  const dispatch = createEventDispatcher();

  function handleDrawerClick(index) {
    dispatch("drawerClick", index); // this is what Main is listening for
  }
</script>

<div class="cabinet">
  {#each mockData as item, index}
    <Drawer
      category={item.category}
      id={index}
      isActive={activeDrawer === index}
      on:click={() => handleDrawerClick(index)}
    />
  {/each}
</div>

<style>
  .cabinet {
    background-color: #202020;
    width: 250px;
    height: 80%;
    padding: 10px;
    margin: 4rem 2rem;
    border-radius: 3px;
  }

  @media (max-width: 900px) {
    .cabinet {
      width: 100%;
    }
  }
</style>
