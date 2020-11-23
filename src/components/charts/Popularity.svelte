<script>
  import data from "../../data/xd-four-letter-popular-1993.csv";
  $: sliced = data.slice(0, 12);
</script>

<table>
  <thead>
    <th>Answer</th>
    <th>Count</th>
    <th>Percent</th>
  </thead>
  <tbody>
    {#each sliced as { answer, count, percent }}
      <tr>
        <td>{answer}</td>
        <td>{count}</td>
        <td>{percent}</td>
      </tr>
    {/each}
  </tbody>
</table>

<style>
  table {
    max-width: 40em;
    margin: 0 auto;
  }

  td:nth-child(n + 2),
  th:nth-child(n + 2) {
    text-align: right;
    padding: 0.5em;
  }
</style>
