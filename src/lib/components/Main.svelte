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
    activeDrawer !== null ? categoryDescriptions[activeDrawer] : null;

  $: categoryData = selectedCategory
    ? rawData.filter((d) => {
        const agreementString = d.associated_agreement || "";
        const values = agreementString
          .split(";")
          .map((v) => v.trim().toLowerCase());
        return selectedCategory.aliases.some((alias) =>
          values.includes(alias.toLowerCase())
        );
      })
    : [];

  let activeDrawer = null;

  function handleDrawerClick(id) {
    activeDrawer = activeDrawer === id ? null : id;
  }

  const categoryDescriptions = [
    {
      key: "BWC",
      label: "BWC",
      full_name: "Biological Weapons Convention",
      description:
        "Materials and related files from the Biological Weapons Convention.",
      aliases: ["BWC"],
    },
    {
      key: "CWC",
      label: "CWC",
      full_name: "Chemical Weapons Convention",
      description: "Agreements and notes from the Chemical Weapons Convention.",
      aliases: ["CWC"],
    },
    {
      key: "INF",
      label: "INF",
      full_name: "Intermediate-Range Nuclear Forces Treaty",
      description: "Documents from the INF Treaty.",
      aliases: ["INF"],
    },
    {
      key: "PNIs",
      label: "PNI's",
      full_name: "Presidential Nuclear Initiatives",
      description: "Records from the Presidential Nuclear Initiatives.",
      aliases: ["PNIs"],
    },
    {
      key: "START",
      label: "START",
      full_name: "Strategic Arms Reduction Treaty",
      description: "Files from the START agreements.",
      aliases: ["START", "START 1", "START 2", "New START"], // <---
    },
  ];
</script>

<header class="site-header">
  <img src="/assets/logo.svg" alt="Site Header" class="site-header__logo" />
</header>
<section class="hero">
  <div class="hero__content">
    <h1>Arms Control Treaty Archive</h1>
    <p>
      A historical record of major multilateral and bilateral arms control
      agreements.
    </p>
  </div>
</section>
<div class="wrapper">
  <div class="main">
    <Cabinet
      categories={categoryDescriptions}
      on:drawerClick={(e) => handleDrawerClick(e.detail)}
      {activeDrawer}
    />
    <div class="folder-area" style="--folder-width: 45%;">
      <div class="category-details-wrapper">
        {#if activeDrawer !== null && categoryData.length > 0}
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
  :global(html) {
    box-sizing: border-box;
  }

  :global(*),
  :global(*::before),
  :global(*::after) {
    box-sizing: inherit;
  }
  :global(body) {
    margin: 0;
    /* overflow: hidden; */
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
    box-sizing: border-box;
    position: sticky;
    top: 0;
    z-index: 999;
    width: 100%;
    background: #162140;
    color: white;
    height: 80px;
    padding: 1rem 2rem;
    /* border-bottom: 1px solid #826022; */
    font-family: "IBM Plex Sans", sans-serif;
  }
  .wrapper {
    /* max-width: 1900px; */
    height: calc(100vh - 100px);
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
    height: 87%;
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

  /* ------------------------ Hero ------------------------ */
  .hero {
    height: 100vh;
    background-image: url("../assets/cover.jpg");
    background-size: cover;
    background-position: center;
    color: black;
    padding: 4rem 2rem;
    text-align: center;
    font-family: "Impact Label", sans-serif;
    box-shadow: inset 0 -3px 10px rgba(0, 0, 0, 0.3);
    display: flex;
    align-items: center; /* vertically center content */
    justify-content: center; /* horizontally center content */
  }

  .hero__content {
    max-width: 900px;
    margin: 0 auto;
  }

  .hero h1 {
    font-size: 7rem;
    margin-bottom: 3rem;
    line-height: 1.5;
  }

  .hero p {
    font-size: 3.25rem;
    margin: 0;
    line-height: 1.5;
  }
</style>
