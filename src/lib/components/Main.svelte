<script>
  import Cabinet from "./Cabinet.svelte";
  import Folder from "./Folder.svelte";

  let folders = [
    { id: 1, label: "Pre-Negotiation" },
    { id: 2, label: "Negotiation" },
    { id: 3, label: "Implementation" },
    { id: 4, label: "Dispute Resolution" },
  ];

  let activeId = null;
</script>

<header class="site-header">
  <img src="/assets/logo.svg" alt="Site Header" class="site-header__logo" />
</header>
<div class="wrapper">
  <div class="main">
    <Cabinet />
    <div class="folder-area">
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
