<script>
  import { format } from "d3-format";
  import { scaleLinear } from "d3-scale";
  import data from "../../data/xd-four-letter-popular-1993.csv";
  $: sliced = data.slice(0, 10);
  $: domain = [0, +sliced[0].percent];
  $: scale = scaleLinear().domain(domain).range([0, 100]);
</script>

<div>
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
          <td><span style="width: {scale(+percent)}%;">{percent}%</span></td>
        </tr>
      {/each}
    </tbody>
  </table>
</div>

<style>
  div {
    max-width: 35em;
    margin: 0 auto;
    padding: 0 1em;
  }

  table {
    width: 100%;
    font-size: 0.85em;
    margin: 0 auto;
  }

  .highlight {
    font-weight: var(--bold);
    background-color: var(--highlight);
  }

  tr {
    border-bottom: 1px dashed var(--default);
  }

  thead {
    border-bottom-width: 2px;
  }

  tr:last-of-type {
    border: none;
  }

  td:nth-child(n + 2),
  th:nth-child(n + 2) {
    text-align: right;
    padding: 0.5em;
  }

  td:nth-child(1),
  th:nth-child(1) {
    vertical-align: middle;
  }

  td:nth-child(3),
  th:nth-child(3) {
    width: 15em;
    padding-left: 2em;
    display: none;
  }

  span {
    display: inline-block;
    height: 100%;
    background-color: var(--default);
    padding: 0.25em;
    padding-right: 0.5em;
    padding-top: 0.375em;
    line-height: 1;
    color: var(--white);
    border-radius: 4px;
  }

  @media only screen and (min-width: 640px) {
    table {
      width: 100%;
    }

    td:nth-child(3),
    th:nth-child(3) {
      display: table-cell;
    }
  }
</style>
