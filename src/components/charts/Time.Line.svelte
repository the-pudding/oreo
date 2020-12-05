<script>
  import { getContext } from "svelte";
  import { line, curveCardinal } from "d3-shape";

  const { data, xGet, yGet, yScale, xScale } = getContext("LayerCake");

  $: path = line().x($xGet).y($yGet).curve(curveCardinal.tension(0.75));
</script>

{#each $data as { name, values }}
  <g transform="translate(0, -1)">
    <path class="{name} bg" d="{path(values)}"></path>
    <path class="{name} fg" d="{path(values)}"></path>
  </g>
{/each}

<style>
  path {
    fill: none;
    stroke-linejoin: round;
    stroke-linecap: round;
    stroke-width: 2px;
  }

  .cookie {
    stroke: var(--fg);
    stroke-width: 4px;
  }

  .mountain {
    stroke: var(--default);
  }

  .mountain.bg {
    display: none;
  }

  .bg {
    stroke-width: 12px;
    stroke: var(--highlight);
  }
</style>
