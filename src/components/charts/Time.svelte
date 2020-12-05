<script>
  import { LayerCake, Svg } from "layercake";
  import { max, extent } from "d3-array";
  import Line from "./Time.Line.svelte";
  import AxisX from "./Time.AxisX.svelte";
  import AxisY from "./Time.AxisY.svelte";
  import raw from "../../data/xd-nyt-oreo-1950.csv";

  let w;

  const clean = raw.map((d) => ({
    ...d,
    year: +d.year,
    four: +d.four,
    cookie: +d.cookie,
    mountain: +d.mountain,
  }));

  const data = ["mountain", "cookie"].map((prop) => ({
    name: prop,
    values: clean.map((d) => ({
      year: d.year,
      count: d[prop],
      percent: d[prop] / d.four,
    })),
  }));

  const flat = [].concat(...data.map((d) => d.values));

  const xDomain = extent(flat, (d) => d.year);
  const yDomain = [0, max(flat, (d) => d.percent)];
</script>

<div class="chart" bind:clientWidth="{w}">
  <LayerCake
    padding="{{ top: 10, right: 10, bottom: 20, left: 20 }}"
    x="{'year'}"
    y="{'percent'}"
    xDomain="{xDomain}"
    yDomain="{yDomain}"
    yPadding="{[10, 0]}"
    data="{data}">
    <Svg>
      <AxisX />
      <AxisY />
      <Line />
    </Svg>
  </LayerCake>
</div>

<style>
  .chart {
    height: 50vh;
    padding: 0 2rem;
  }
</style>
