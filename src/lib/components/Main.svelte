<script>
  import Cabinet from "./Cabinet.svelte";
  import Folder from "./Folder.svelte";
  import CategoryDetails from "./CategoryDetails.svelte";
  import getData from "../data.js";
  import { onMount } from "svelte";

  let rawData = [];

  onMount(async () => {
    const result = await getData();
    rawData = result.data;
  });

  let folders = [
    { id: 1, label: "Pre-Negotiation" },
    { id: 2, label: "Negotiation" },
    { id: 3, label: "Implementation" },
    { id: 4, label: "Dispute Resolution" },
  ];

  $: selectedCategory =
    activeDrawer !== null ? categoryDescriptions[activeDrawer]?.label : null;

  $: categoryData = selectedCategory
    ? rawData.filter(
        (d) =>
          d.associated_agreement &&
          d.associated_agreement
            .split(";")
            .some(
              (val) =>
                val.trim().toLowerCase() === selectedCategory.toLowerCase()
            )
      )
    : [];

  let activeDrawer = null;

  function handleDrawerClick(id) {
    activeDrawer = activeDrawer === id ? null : id;
  }

  const categoryDescriptions = [
    {
      label: "BWC",
      full_name: "Biological Weapons Convention",
      description:
        "Materials and related files from the Biological Weapons Convention.",
    },
    {
      label: "CWC",
      full_name: "Chemical Weapons Convention",
      description: "Agreements and notes from the Chemical Weapons Convention.",
    },
    {
      label: "INF",
      full_name: "Intermediate-Range Nuclear Forces Treaty",
      description: "Documents from the INF Treaty.",
    },
    {
      label: "PNI'S",
      full_name: "Presidential Nuclear Initiatives",
      description: "Records from the Presidential Nuclear Initiatives.",
    },
    {
      label: "START",
      full_name: "Strategic Arms Reduction Treaty",
      description: "Files from the START agreements.",
    },
  ];
</script>

<header class="site-header">
  <img src="/assets/logo.svg" alt="Site Header" class="site-header__logo" />
</header>
<div class="wrapper">
  <div class="main">
    <Cabinet
      on:drawerClick={(e) => handleDrawerClick(e.detail)}
      {activeDrawer}
    />
    <div class="folder-area" style="--folder-width: 45%;">
      <div class="category-details-wrapper">
        {#if activeDrawer !== null}
          <CategoryDetails
            category={categoryDescriptions[activeDrawer].label}
            full_name={categoryDescriptions[activeDrawer].full_name}
            description={categoryDescriptions[activeDrawer].description}
            data={categoryData}
          />
        {/if}
      </div>

      <Folder
        phases={[
          "Pre-Negotiation",
          "Negotiation",
          "Implementation",
          "Dispute Resolution",
        ]}
      />
    </div>
  </div>
</div>

<style>
  :global(body) {
    margin: 0;
    overflow: hidden;
    background: #d2d0d0;
  }

  :global {
    @font-face {
      font-family: "Impact Label";
      src: url("/assets/impactLabel.ttf") format("truetype");
      font-weight: normal;
      font-style: normal;
    }
  }

  .site-header {
    position: sticky;
    top: 0;
    z-index: 999;
    width: 100%;
    background: #162140;
    color: white;
    height: 60px;
    padding: 1rem 2rem;
    /* border-bottom: 1px solid #826022; */
    font-family: "IBM Plex Sans", sans-serif;
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
    position: relative;
    background-image: url("../assets/dark_wood.jpeg");
    background-size: cover;
    background-position: center;
    flex: 1;
    overflow-y: auto;
    padding: 1rem;
    box-sizing: border-box;
  }

  .category-details-wrapper {
    position: absolute;
    z-index: 10; /* ensure it sits *above* the folder visually */
    pointer-events: none; /* so it doesn’t block folder clicks */
    width: 80%;
    left: 0;
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
