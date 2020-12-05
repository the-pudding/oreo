<script>
  import { getContext } from "svelte";

  const { data, xScale, yScale } = getContext("LayerCake");
  export let x1;
  export let x2;
  export let y1;
  export let y2;
</script>

<line
  x1="{$xScale(x1)}"
  y1="{$yScale(y1)}"
  x2="{$xScale(x2)}"
  y2="{$yScale(y2)}"></line>

<style>
  line {
    fill: none;
    stroke-linejoin: round;
    stroke-linecap: round;
    stroke-width: 2px;
    stroke: var(--fg);
  }
</style>
