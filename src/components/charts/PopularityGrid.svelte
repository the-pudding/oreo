<script>
  import { format } from "d3-format";
  import { scaleLinear } from "d3-scale";
  import { group } from "d3-array";
  import data from "../../data/xd-four-letter-popular-1993.csv";

  const itemW = 105;
  let w = itemW;

  $: x = Math.floor(w / itemW);
  $: count = x * 4;
  $: sliced = data.slice(0, count);
  $: grouped = group(sliced, (d) => Math.floor(count / 1000));
  $: console.log(grouped);
  $: domain = [+sliced[count - 1].count, +sliced[0].count];
  // $: domain = [0, +sliced[0].count];
  $: scale = scaleLinear().domain(domain).range([0, 100]);
</script>

<div class="outer">
  <div class="grid" bind:clientWidth="{w}">
    {#each sliced as { answer, count }, i}
      <div class="item" class:highlight="{answer === 'OREO'}">
        <span class="bg" style="opacity: {scale(+count)}%;"></span>
        <span class="answer">{answer}</span>
        <span class="count">{format(',')(count)}</span>
        <span class="rank">{i + 1}</span>
      </div>
    {/each}
  </div>
</div>

<style>
  .outer {
    padding: 1em;
  }

  .grid {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }

  .item {
    position: relative;
    padding: 1em;
    box-shadow: 0 0 1px 0 var(--fg);
    margin: 1px;
  }

  span {
    width: 3em;
    display: block;
    text-align: center;
    color: var(--fg);
    position: relative;
    line-height: 1;
  }

  .bg {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: var(--highlight);
  }

  .highlight {
    box-shadow: 0 0 0 4px var(--fg);
    z-index: var(--z-top);
  }

  .answer {
    font-weight: var(--bold);
  }

  .count {
    margin-top: 0.5em;
    font-size: 0.8em;
  }

  .rank {
    position: absolute;
    top: 0.5em;
    left: 0.5em;
    line-height: 1;
    font-size: 0.5em;
    opacity: 0.75;
  }
</style>
