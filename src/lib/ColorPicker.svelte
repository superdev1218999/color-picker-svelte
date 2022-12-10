<script>
  let selectedColor = "#B53FFE";
  let colors = JSON.parse(localStorage.getItem("colors"))
    ? JSON.parse(localStorage.getItem("colors"))
    : [];
  $: {
    window.localStorage.setItem("colors", JSON.stringify(colors));
  }
  const saveColor = () => {
    colors = [selectedColor, ...colors];
  };
  const copyColor = (index) => {
    navigator.clipboard.writeText(colors[index]);
  };
  const deleteColor = (index) => {
    colors.splice(index, 1);
    colors = colors;
  };
</script>

<div class="main">
  <div class="color-picker pt_text-center">
    <input type="color" id="colorpicker" bind:value={selectedColor} />
    <br />
    <button class="pt_button pt_button-green pt_mt-2rem" on:click={saveColor}>
      Save
    </button>
  </div>

  <div class="color-list">
    {#each colors as color, index}
      <div class="color-item">
        <div
          class="color-div"
          on:click={() => {
            copyColor(index);
          }}
          style="background-color: {color};"
        />
        <button
          class="pt_button pt_button-blue"
          on:click={() => {
            copyColor(index);
          }}>Copy</button
        >
        <button
          class="pt_button pt_button-red"
          on:click={() => {
            deleteColor(index);
          }}>Delete</button
        >
      </div>
    {/each}
  </div>
</div>

<style>
  .main {
    margin-top: 3rem;
    display: flex;
    gap: 1rem;
    justify-content: space-between;
  }
  .color-list {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    flex: 1;
  }
  .color-item {
    display: flex;
    flex-direction: row;
    gap: 1rem;
    justify-content: space-between;
  }
  .color-item .color-div {
    border-radius: 10px;
    min-width: 100px;
    flex: 1;
    border: 1px #ff3e00aa solid;
    cursor: pointer;
  }
  #colorpicker {
    width: 100px;
    height: 100px;
  }
</style>
