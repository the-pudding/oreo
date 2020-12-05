<script>
  import { getContext } from "svelte";
  import { scaleLinear } from "d3-scale";
  import { line, curveCardinal } from "d3-shape";

  const { data, xGet, yGet, yScale, xScale } = getContext("LayerCake");

  $: path = line().x($xGet).y($yGet).curve(curveCardinal.tension(0.5));
</script>

{#each $data as { name, values }}
  <path class="{name}" d="{path(values)}"></path>
{/each}

<style>
  path {
    fill: none;
    stroke-linejoin: round;
    stroke-linecap: round;
    stroke-width: 2px;
  }

  .cookie {
    stroke: var(--primary);
    stroke-width: 4px;
  }

  .mountain {
    stroke: var(--default);
  }
</style>
