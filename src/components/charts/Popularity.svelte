<script>
  import { format } from "d3-format";
  import { scaleLinear } from "d3-scale";
  import data from "../../data/xd-four-letter-popular-1993.csv";
  $: sliced = data.slice(0, 12);
  $: domain = [0, +sliced[0].percent];
  $: scale = scaleLinear().domain(domain).range([0, 100]);
</script>

<table>
  <thead>
    <th>Answer</th>
    <th>Count</th>
    <th>Percent</th>
  </thead>
  <tbody>
    {#each sliced as { answer, count, percent }}
      <tr class:highlight="{answer === 'OREO'}">
        <td>{answer}</td>
        <td>{format(',')(count)}</td>
        <td><span style="width: {scale(+percent)}%;">{percent}</span></td>
      </tr>
    {/each}
  </tbody>
</table>

<style>
  table {
    max-width: 30em;
    margin: 0 auto;
  }
  .highlight {
    font-weight: var(--bold);
  }
  td:nth-child(n + 2),
  th:nth-child(n + 2) {
    text-align: right;
    padding: 0.5em;
  }
  td:nth-child(1),
  th:nth-child(1) {
    width: 5em;
  }
  td:nth-child(3),
  th:nth-child(3) {
    width: 15em;
    padding-left: 2em;
  }
  span {
    display: inline-block;
    height: 100%;
    background-color: pink;
    padding-right: 0.5em;
  }
</style>
