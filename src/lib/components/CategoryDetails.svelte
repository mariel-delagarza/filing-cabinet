<script>
  export let category;
  export let description;
  export let full_name;
  export let data = [];

  console.log("CategoryDetails data:", data);

  $: totalDocuments = data.length;

  $: types = [...new Set(data.map((item) => item.type))];

  let names = [
    ...new Map(
      data
        .flatMap((item) => item.names || [])
        .map((person) => [person.name.toLowerCase(), person]) // use name as key
    ).values(),
  ];
  // let names = [...new Set(data.map((item) => item.names).flat())];
  console.log("Names:", names);
</script>

<div class="category-details">
  <div class="category-header">
    <h2 class="bold">{category}</h2>
    <h3>{full_name}</h3>
    <p>{description}</p>
  </div>
  <div class="category-content">
    <p><span class="bold">Total documents:</span> {totalDocuments}</p>
    <p><span class="bold">Types of documents:</span></p>
    <ul>
      {#each types as type}
        <li>{type}</li>
      {/each}
    </ul>
    <p><span class="bold">People involved:</span></p>
    <ul>
      {#each names
        .slice() // create a copy so we don’t mutate the original
        .sort((a, b) => a.name.localeCompare(b.name)) as person}
        <li>{person.name}</li>
      {/each}
    </ul>
  </div>
</div>

<style>
  .category-header {
    margin-bottom: 20px;
  }

  .category-details {
    background-image: url("../assets/oldpaper.jpg");
    background-size: cover;
    background-position: center;
    padding: 1rem;
    box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3);
    font-family: "Special Elite", serif;
    font-size: 1rem;
    width: calc(var(--folder-width));
    margin-left: 2rem;
    margin-top: 4rem;
    line-height: 1.7;
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
  h3 {
    margin: 0;
  }
</style>
