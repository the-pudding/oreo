<script>
  import { onMount } from "svelte";
  import { format } from "d3-format";
  import { scaleLinear } from "d3-scale";
  import { group } from "d3-array";
  import data from "../../data/xd-four-letter-popular-1993.csv";

  const itemW = 74;
  const rows = 4;
  let w;
  let scale;
  let sliced = [];
  let mounted = false;

  $: if (w) {
    const x = Math.floor(w / itemW);
    const c = x * rows;
    sliced = data.slice(0, c);
    const domain = [+sliced[c - 1].count, +sliced[0].count];
    scale = scaleLinear().domain(domain).range([0, 100]);
  }

  onMount(() => {
    mounted = true;
  });
</script>

{#if mounted}
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
{/if}

<style>
  .outer {
    padding: 1em;
    margin: 0 auto;
    max-width: 60em;
    width: 100%;
  }

  .grid {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    width: 100%;
  }

  .item {
    display: flex;
    flex-direction: column;
    justify-content: center;
    position: relative;
    box-shadow: 0 0 1px 0 var(--fg);
    margin: 1px;
    width: 72px;
    height: 72px;
    font-size: 18px;
    border-radius: 4px;
  }

  span {
    display: block;
    text-align: center;
    color: var(--fg);
    position: relative;
    line-height: 1;
    width: 100%;
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
    margin-top: 0.5em;
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
    text-align: left;
  }
</style>
