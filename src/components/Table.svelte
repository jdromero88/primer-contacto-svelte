<script>
  import Search from './Search.svelte'
  import Select from './Select.svelte'
  export let satellites
  export let search
  export let selectOptions
  export let selected
</script>

<Search search={search} />
<Select
  selectOptions={selectOptions}
  selected={selected}
/>
<div>
  <table>
    <thead>
      <tr>
        <th colspan="5">Satellites</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Name</td>
        <td>Norad ID</td>
        <td>Country of Launch</td>
        <td>Orbit Type</td>
        <td>Launch Date</td>
      </tr>
      {#each satellites as sat}
        <tr>
          <td>{(sat.ag_meta.Name ? sat.ag_meta.Name : 'No Data')}</td>
          <td>{(sat.ag_meta.NoradId ? sat.ag_meta.NoradId : 'No Data')}</td>
          <td>{(sat.ag_meta.countryOfLaunch ? sat.ag_meta.countryOfLaunch : 'No Data')}</td>
          <td>{(sat.ag_meta.OrbitType ? sat.ag_meta.OrbitType : 'No Data')}</td>
          <td>{(sat.ag_meta.LaunchDate ? sat.ag_meta.LaunchDate : 'No Data')}</td>
        </tr>
      {/each }
    </tbody>
    <tfoot>
      <tr>
        <td colspan="5">este es el footer!</td>
      </tr>
    </tfoot>
  </table>
</div>
<style>
  div {
    display: flex;
    justify-content: center;
  }
  table,
  td {
      border: 1px solid #333;
  }

  thead,
  tfoot {
      background-color: #333;
      color: #fff;
  }
</style>