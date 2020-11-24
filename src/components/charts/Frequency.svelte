<script>
  import { format } from "d3-format";
  import { scaleLinear } from "d3-scale";
  import data from "../../data/xd-letter-freq-1993.csv";
  $: domain = [0, +data[0].percent];
  $: scale = scaleLinear().domain(domain).range([0, 100]);
  $: highlight = ["O", "R", "E"];
</script>

<div class="chart">
  {#each data as { letter, freq, percent } (letter)}
    <div
      class="item item--{letter}"
      class:highlight="{highlight.includes(letter)}">
      <span class="letter">{letter}</span>
      <span class="bar" style="height: {scale(+percent)}%;">
        <span class="percent">{format('.1%')(percent)}</span>
      </span>
    </div>
  {/each}
</div>

<style>
  .chart {
    height: 50vh;
    display: flex;
    margin-top: 1.25em;
    cursor: crosshair;
  }

  .item {
    width: 3.5vw;
    border: 1px solid var(--bg);
    text-align: center;
    display: flex;
    flex-direction: column-reverse;
  }

  .bar {
    display: block;
    background: var(--default);
    position: relative;
  }

  .percent {
    position: absolute;
    top: 0;
    left: 0;
    transform: translate(0, -1.25em);
    opacity: 0;
    font-size: 0.8em;
  }

  .highlight.item--R .percent {
    opacity: 0;
  }

  .highlight .bar {
    background: var(--primary);
  }

  .highlight .percent {
    opacity: 1;
  }

  .highlight .letter {
    font-weight: var(--bold);
  }

  .item:hover .percent {
    opacity: 1;
  }
</style>
