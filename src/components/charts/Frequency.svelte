<script>
  import { format } from "d3-format";
  import { scaleLinear } from "d3-scale";
  import { onMount } from "svelte";
  import data from "../../data/xd-letter-freq-1993.csv";

  $: domain = [0, +data[0].percent];
  $: scale = scaleLinear().domain(domain).range([0, 100]);
  $: highlight = ["O", "R", "E"];
</script>

<div class="outer">
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
</div>

<style>
  .outer {
    margin-top: 1.25em;
    max-width: 60em;
    margin: 0 auto;
    padding: 1em;
  }
  .chart {
    height: 50vh;
    display: flex;
    cursor: crosshair;
  }

  .item {
    width: calc(1 / 26 * 100%);
    border: 2px solid var(--bg);
    text-align: center;
    display: flex;
    flex-direction: column-reverse;
  }

  .bar {
    display: block;
    background: var(--default);
    position: relative;
    border-radius: 4px;
  }

  .percent {
    position: absolute;
    top: 0;
    left: 0;
    transform: translate(0, -1.25em);
    opacity: 0;
    font-size: 0.75em;
    width: auto;
    transition: all 150ms ease-in-out;
    overflow: visible;
    font-weight: var(--bold);
  }

  .letter {
    line-height: 1;
    padding: 0.5em 0 0.375em 0;
    margin-top: 0.25em;
    transition: all 50ms ease-in-out;
    border-radius: 4px;
  }

  .highlight.item--R .percent {
    opacity: 0;
  }

  .highlight .bar {
    background: var(--fg);
  }

  .highlight .percent {
    opacity: 1;
  }

  .highlight .letter {
    font-weight: var(--bold);
    /* transform: scale(1.5) translateY(12.5%); */
    background: var(--highlight);
  }

  .item:hover .percent {
    opacity: 1;
  }

  .item:hover .letter {
    font-weight: var(--bold);
    background: var(--fg);
    color: var(--bg);
  }

  @media only screen and (min-width: 1280px) {
    .highlight.item--R .percent {
      opacity: 1;
    }
    .percent {
      left: 50%;
      transform: translate(-50%, -1.25em);
    }
  }
</style>
