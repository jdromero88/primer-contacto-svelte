<script> 
  export let selected
  export let selectOptions
</script>

<label for="country-of-launch-select" aria-hidden="true" hidden>Filter by Pronouns</label>
<select name="countries" id="country-of-launch-select" on:change={selected}>
  <option value="">Select a Pronouns</option>
  <option value="">All</option>
  {#each selectOptions as val}
    <option value="{val}">{(val ? val : 'No Data' )}</option>
  {/each}
</select>

<style>
  label[aria-hidden="true"],
  [hidden] {
    display: none;
  }
</style>