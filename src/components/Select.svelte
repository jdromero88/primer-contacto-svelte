<script>
  // import { onMount } from 'svelte'
  
  export let selected
  export let selectOptions
  // onMount( () => {
  //   if (satellites)
  //     console.log(satellites)
  // })
</script>

<label for="country-of-launch-select" aria-hidden="true" hidden>Filter by Country of Launch</label>
<select name="countries" id="country-of-launch-select" on:change={selected}>
  <option value="">Select a Country of Launch</option>
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