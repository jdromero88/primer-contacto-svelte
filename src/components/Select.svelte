<script> 
  export let selected
  export let selectOptions
</script>

<label for="pronouns-select" aria-hidden="true" hidden>Filter by Pronouns</label>
<select name="pronouns" id="pronouns-select" on:change={selected}>
  <option value="">Select a Pronoun</option>
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