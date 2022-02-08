<script>
  import Search from './Search.svelte'
  export let satellites
</script>

<Search satellites = {satellites} />
<div>
  <table>
    <thead>
      <tr>
        <th colspan="6">Titulo de la tabla!</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>uno</td>
        <td>dos</td>
        <td>tres</td>
        <td>cuatro</td>
        <td>cinco</td>
        <td>seis</td>
      </tr>
    </tbody>
    <tfoot>
      <tr>
        <td colspan="6">este es el footer!</td>
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