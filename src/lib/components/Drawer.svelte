<script>
  export let category;

  let selectedId = null;
</script>

<div class="drawer">
  <div class="wrapper">
    <div class="drawer-label">
      <span id="drawer-label-text">{category}</span>
    </div>
    <div class="drawer-handle"></div>
  </div>

  <div class="files"></div>
</div>

<style>
  .drawer {
    position: relative;
    width: 96%;
    height: 19.5%;
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

  .drawer-label {
    text-align: center;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 50px;
    padding: 0.25rem 0; /* optional: add top/bottom breathing room */

    border: 2px solid #dddddd;
    margin: 0 auto 30px auto;
    box-shadow: inset 0px 0px 5px rgba(0, 0, 0, 1);
  }

  #drawer-label-text {
    font-family: "Impact Label", sans-serif;
    background: #111;
    color: white;
    /* padding: 0.25rem 0.5rem; */
    font-size: 2.25rem;
    line-height: 1;
    display: inline-block;
    transform: rotate(-1deg);
    /* box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.4); */
    filter: invert(1) brightness(1.5); /* Key */
  }

  .drawer-handle {
    display: block;
    position: relative;
    background: linear-gradient(to bottom, #dddddd 0%, #5e5e5e 100%);
    width: 100%;
    height: 7px;
    box-shadow: 0px 0px 5px rgba(0, 0, 0, 1);
  }

  .wrapper {
    margin: 0 auto;
    top: 50%;
    transform: translateY(-50%);
    position: relative;
    width: 120px;
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
    content: "";
    position: absolute;
    top: -10px;
    height: 10px;
    width: 50%;
    box-shadow: -1px -2px 5px rgba(0, 0, 0, 0.2);
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
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
