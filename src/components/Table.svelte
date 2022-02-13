<script>
  import Search from './Search.svelte'
  import Select from './Select.svelte'
  export let dataset
  export let search
  export let selectOptions
  export let selected
  export let options
  export let searchBy
</script>

<Search
  search={search}
  options={options}
  searchBy={searchBy}
/>
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
        <td>F Name</td>
        <td>L Name</td>
        <td>Cohort</td>
        <td>Pronouns</td>
        <td>Username</td>
      </tr>
      {#each dataset.users as user}
        <tr>
          <td>{(user.first_name ? user.first_name : 'No Data')}</td>
          <td>{(user.last_name ? user.last_name : 'No Data')}</td>
          <td>{(user.cohort.name ? user.cohort.name : 'No Data')}</td>
          <td>{(user.pronouns ? user.pronouns : 'No Data')}</td>
          <td>{(user.username ? user.username : 'No Data')}</td>
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