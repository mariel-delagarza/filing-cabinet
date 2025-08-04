<script lang="ts">
  export let label: string;
  export let isOpen: boolean = false;
  export let onClick: () => void;
</script>

<div class="folder {isOpen ? 'open' : ''}">
  <div class="tab" on:click={onClick}>
    {label}
  </div>
  <div class="body">
    <!-- stuff inside folder like post-its or document goes here later -->
  </div>
</div>

<style>
.folder {
  position: relative;
  display: flex;
  flex-direction: row;
  align-items: flex-start;
  transition: transform 0.3s ease;
}

/* Folder tab */
.tab {
  writing-mode: vertical-rl;
  transform: rotate(180deg);
  background: #fdfadd;
  border: 2px solid #ccc;
  border-left: 6px solid #aaa;
  border-radius: 0.5rem 0 0 0.5rem;
  padding: 1rem 0.75rem;
  font-size: 0.75rem;
  font-weight: bold;
  cursor: pointer;
  box-shadow: 2px 2px 5px rgba(0,0,0,0.1);
  z-index: 2;
}

/* Folder body */
.body {
  width: 0;
  height: 10rem;
  overflow: hidden;
  background: rgba(0, 0, 255, 0.2); /* temp see-through blue */
  transition: width 0.3s ease;
  border: 1px solid transparent;
  background-image: url('/src/assets/light_wood.jpeg');
  background-size: cover;
}

/* Open folder */
.open .body {
  width: 30rem;
  border: 1px solid #999;
}
</style>
