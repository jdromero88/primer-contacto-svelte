<script>
  export let search
  export let options
  export let searchBy
</script>

<div>
  <label for="search" aria-hidden="true" hidden>Search</label>
  <input type="search" name="search" id="search" placeholder="Search..." on:input={search}>
  
  <label for="filter-by-select" aria-hidden="true" hidden>Filter by</label>
  <select name="filter" id="filter-by-select" on:change={searchBy}>
    {#each options as val}
      <option value="{val}">{val}</option>
    {/each}
  </select>
</div>

<style>
label[aria-hidden="true"],
[hidden] {
  display: none;
}
</style>
