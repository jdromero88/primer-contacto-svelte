<script>
  export let satellites
  // const SEARCH = document.querySelector('#search')
  // SEARCH.addEventListener('input', handleSearch)
  console.log(satellites);

  function handleSearch(e) {
    let searchID = e.target.value
    // console.log(searchID);
    // console.log(satellites);
    const result = satellites.filter(s => s.id.toString().includes(searchID))
    console.log(result);
  }
</script>

<div>
  <label for="search" aria-hidden="true" hidden>Search:</label>
  <input type="search" name="search" id="search" placeholder="Search..." on:input={handleSearch}>
</div>

<style>
label[aria-hidden="true"],
[hidden] {
  display: none;
}
</style>
