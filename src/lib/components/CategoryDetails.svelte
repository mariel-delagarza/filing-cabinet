<script>
  export let category;
  export let description;
  export let full_name;
  export let data = [];

  console.log("CategoryDetails data:", data);

  let totalDocuments = data.length;
  console.log("Total documents:", totalDocuments);

  let types = [...new Set(data.map((item) => item.type))];
  console.log("Types of documents:", types);

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
  <h2>{category}</h2>
  <h3>{full_name}</h3>
  <p>{description}</p>
  <p>Total documents: {totalDocuments}</p>
  <p>Types of documents: {types.join(", ")}</p>
</div>

<style>
  .category-details {
    background-image: url("../assets/oldpaper.jpg");
    background-size: cover;
    background-position: center;
    padding: 1rem;
    box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3);
    font-family: "Special Elite", serif;
    width: calc(var(--folder-width));
    margin-left: 2rem;
    margin-top: 4rem;
    line-height: 1.7;
  }

  h2 {
    font-size: 1.5rem;
    margin: 0;
  }

  h3 {
    margin: 0;
  }

  p {
    font-size: 1rem;
    margin: 0;
  }
</style>
