<script>
  import PostIt from "./PostIt.svelte";
  // export let category;
  export let description;
  export let full_name;
  export let data = [];

  console.log("CategoryDetails data:", data);

  $: totalDocuments = data.length;

  $: types = [...new Set(data.map((item) => item.type))];

  $: names = [
    ...new Map(
      data
        .flatMap((item) => item.names || [])
        .filter((person) => person.name && person.name.trim() !== "") // remove empty names
        .map((person) => [person.name.toLowerCase(), person])
    ).values(),
  ];
  $: if (names) {
    console.log("Names:", names);
  }

  $: tags = [
    ...new Set(
      data
        .flatMap((item) => item.content_tags || []) // flatten all tags into one array
        .map((tag) => tag.trim())
        .filter((tag) => tag !== "") // remove empty strings
    ),
  ];

  $: sortedTags = tags.slice().sort((a, b) => a.localeCompare(b));
  $: if (sortedTags) {
    console.log("Sorted Tags:", sortedTags);
  }
  $: dates = data
    .map((item) => new Date(item.date))
    .filter((date) => !isNaN(date)); // remove invalid dates

  $: earliestDate = dates.length ? new Date(Math.min(...dates)) : null;

  $: latestDate = dates.length ? new Date(Math.max(...dates)) : null;

  function formatDate(date) {
    return date.toLocaleDateString("en-US", {
      year: "numeric",
      month: "short",
      day: "numeric",
    });
  }

  $: formattedStartDate = formatDate(earliestDate);
  $: formattedEndDate = formatDate(latestDate);
</script>

<div class="category-details">
  <div class="category-header">
    <h2 class="bold">{full_name}</h2>
    <p class="category-header__description">{description}</p>
  </div>

  <div class="category-content">
    <div class="category-meta">
      <p><span class="bold">Total documents:</span> {totalDocuments}</p>
      <p><span class="bold">Types of documents:</span></p>
      <ul>
        {#each types as type}
          <li>{type}</li>
        {/each}
      </ul>
    </div>
    <div class="postit-wrapper">
      <div id="postit-1">
        <PostIt startDate={formattedStartDate} endDate={formattedEndDate} />
      </div>
      <div id="postit-2">
        <PostIt tags={sortedTags.slice(0, 6)} />
        {#if sortedTags.length > 6}
          <PostIt tags={sortedTags.slice(6, 15)} />
        {/if}
      </div>
    </div>

    <div class="category-people">
      <p><span class="bold">People involved:</span></p>
      <ul class="names-list">
        {#each names
          .slice() // create a copy so we don’t mutate the original
          .sort((a, b) => a.name.localeCompare(b.name)) as person}
          <li>{person.name}</li>
        {/each}
      </ul>
    </div>
  </div>
</div>

<style>
  .category-details {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    background-image: url("../assets/oldpaper.jpg");
    background-size: cover;
    background-position: center;
    padding: 1rem;
    box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3);
    font-family: "Special Elite", serif;
    font-size: 1rem;
    width: calc(var(--folder-width));
    margin-left: 4rem;
    margin-top: 4rem;
    line-height: 1.7;
    height: 100%;
    overflow: hidden;
    position: relative;
  }

  .bold {
    text-shadow:
      0.5px 0,
      0 -0.5px,
      -0.5px 0,
      0 0.5px;
  }

  .category-details h2 {
    font-size: 1.5rem;
    margin: 0;
  }

  .category-header__description {
    font-size: 1.2rem;
    margin: 0;
    color: #333;
  }
  .category-content {
    flex: 1;
    overflow: hidden;
    flex-direction: column;
    height: 100%;
    display: flex;
  }

  .names-list {
    columns: 2; /* creates two columns */
    column-gap: 2rem; /* space between the columns */
    padding-left: 1rem; /* optional: indent */
    margin: 0;
    max-width: 60%;
  }

  .names-list li {
    break-inside: avoid; /* keeps list items from breaking across columns */
    margin-bottom: 0.25rem;
  }

  @media (max-width: 600px) {
    .names-list {
      columns: 1;
    }
  }

  .category-meta {
    flex: 1;
    overflow: hidden;
  }

  .category-people {
    flex-grow: 0;
    flex-shrink: 0;
    height: 60%;
  }

  .postit-wrapper {
    position: absolute;
    top: 7rem;
    right: 0;
    z-index: 5;
  }

  #postit-1 {
    position: absolute;
    top: 0;
    right: 12rem;
    transform: rotate(2deg);
  }
  #postit-2 {
    position: absolute;
    /* top: 0;
    left: 0; */
    top: 17rem;
    right: 0;
    transform: rotate(-4deg);
  }
</style>
