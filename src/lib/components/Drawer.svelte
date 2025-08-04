<script>
  import Folder from './Folder.svelte';
  export let data;

  let isOpen = false;
</script>


<div class="cabinet">
  <div class="drawer">
    <div class="wrapper">
      <label>{data.category}</label>
      <div class="handle"></div>
    </div>
    <div class="files">
      <span>{data.resource_type}</span>
    </div>
  </div>
</div>


<style>
  * {
    box-sizing: border-box;
  }

  .cabinet {
    background-color: #202020;
    width: 250px;
    height: 400px;
    padding: 10px;
    /* margin: 80px auto; */
    border-radius: 3px;
  }

  .drawer {
    position: relative;
    width: 100%;
    height: 50%;
    border: 2px solid #000000;
    margin: 0 auto;
    background: linear-gradient(135deg, #828282 0%, #202020 40%);
    background-size: 100%;
    transition: all 1s;
    box-shadow: 0 0 0 rgba(0, 0, 0, 0);
    z-index: 1;
  }

  .drawer:hover {
    background-size: 200%;
    transform: scale(1.15);
    z-index: 2;
    box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.7);
  }

  .drawer:hover .files {
    display: block;
    height: 25px;
    top: -27px;
  }

  .wrapper {
    margin: 0 auto;
    top: 50%;
    transform: translateY(-50%);
    position: relative;
    width: 60px;
  }

  label {
    display: block;
    width: 75%;
    height: 30px;
    border: 2px solid #dddddd;
    margin: 0 auto 30px auto;
    box-shadow: inset 0px 0px 5px rgba(0, 0, 0, 1);
  }

  .handle {
    display: block;
    position: relative;
    background: linear-gradient(to bottom, #dddddd 0%, #5e5e5e 100%);
    width: 100%;
    height: 7px;
    box-shadow: 0px 0px 5px rgba(0, 0, 0, 1);
  }

  .files {
    position: absolute;
    background-color: beige;
    width: 95%;
    height: 0;
    left: 0;
    right: 0;
    top: -2px;
    margin: auto;
    box-shadow: -2px -2px 5px rgba(0, 0, 0, 0.2);
    transition: all 1s;
    display: none;
  }

  .files::before,
  .files::after {
    position: absolute;
    top: -10px;
    height: 10px;
    width: 50%;
    box-shadow: -1px -2px 5px rgba(0, 0, 0, 0.2);
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
    content: "";
  }

  .files::before {
    background-color: beige;
    left: 0;
  }

  .files::after {
    background-color: #e5e5c8; /* approximate of darken(beige, 10%) */
    right: 0;
  }
</style>
