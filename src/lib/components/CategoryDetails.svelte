<script>
  export let category;
  export let description;
</script>

<div class="category-details">
  <h2>{category}</h2>
  <p>{description}</p>
</div>

<style>
  .category-details {
    background: #fffdf5;
    border: 2px solid #ccc;
    padding: 1rem;
    box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3);
    font-family: "Source Serif 4", serif;
    /* max-width: 500px; */
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
