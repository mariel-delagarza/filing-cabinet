<script>
  export let category;
  export let description;
  export let full_name;
  export let data = [];

  console.log("CategoryDetails data:", data);
</script>

<div class="category-details">
  <h2>{category}</h2>
  <h3>{full_name}</h3>
  <p>{description}</p>
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
  }

  h2 {
    font-size: 1.5rem;
    margin: 0 0 0.5rem 0;
  }

  p {
    font-size: 1rem;
    margin: 0;
  }
</style>
