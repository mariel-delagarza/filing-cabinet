<script>
  import Drawer from '$lib/components/Drawer.svelte';
  import { mockData } from '$lib/mock/data.js';
</script>

<main>
  <h1>Filing Cabinet MVP</h1>

  <!-- Render the first drawer only -->
  <Drawer data={mockData[0]} />
</main>
