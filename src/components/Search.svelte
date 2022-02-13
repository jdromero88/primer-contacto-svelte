<script>
  export let search
</script>

<div>
  <label for="search" aria-hidden="true" hidden>Search</label>
  <input type="search" name="search" id="search" placeholder="Search..." on:input={search}>
</div>

<style>
label[aria-hidden="true"],
[hidden] {
  display: none;
}
</style>
