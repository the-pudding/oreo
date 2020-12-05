<script>
  import { onMount } from "svelte";
  import { LayerCake, Svg, Canvas } from "layercake";
  import { max, median, mean } from "d3-array";
  import { format } from "d3-format";
  import { scaleLinear, scalePow } from "d3-scale";
  import { line, curveStepBefore } from "d3-shape";
  import { axisLeft, axisBottom } from "d3-axis";
  import { csv } from "d3-fetch";
  import { linearRegression, linearRegressionLine } from "simple-statistics";
  import ScatterCanvas from "./Scatter.Canvas.svelte";
  import AxisX from "./Scatter.AxisX.svelte";
  import AxisY from "./Scatter.AxisY.svelte";
  import Line from "./Scatter.Line.svelte";

  let data = [];
  let highlightData = [];
  let r = 2;
  let fill = "#187aaf";
  let x = "prob";
  let y = "count";

  $: xMax = max(data, (d) => d[x]);
  $: yMax = max(data, (d) => d[y]);
  $: xDomain = [0, xMax];
  $: yDomain = [0, yMax];
  $: xMean = mean(data, (d) => d[x]);
  $: yMean = mean(data, (d) => d[y]);
  $: console.log(xMean, yMean);
  $: regression = linearRegression(data.map((d) => [d[x], d[y]]));
  $: regressionLine = linearRegressionLine(regression);
  $: r1 = regressionLine(0);
  $: r2 = regressionLine(xMax);

  // $: scaleX = scalePow().exponent(0.5).domain(xDomain);

  const cleanAnswers = (arr) => {
    return arr.map((d) => ({
      ...d,
      count: +d.count,
      percent: +d.percent,
      sum: +d.sum,
      prob: +d.prob,
    }));
  };

  onMount(() => {
    csv("assets/data/xd-four-letter-score-1993.csv")
      .then(cleanAnswers)
      .then((result) => {
        data = result;
        highlightData = data.filter((d) => d.answer === "OREO");
      })
      .catch((err) => {
        console.log(err);
      });
  });
</script>

{#if data.length}
  <div class="chart">
    <LayerCake
      padding="{{ top: 10, right: 10, bottom: 20, left: 40 }}"
      x="{x}"
      y="{y}"
      xDomain="{xDomain}"
      yDomain="{yDomain}"
      yPadding="{[r * 2, r * 2]}"
      xPadding="{[r * 2, r * 2]}"
      data="{data}">
      <Canvas>
        <ScatterCanvas r="{r}" fill="{fill}" />
      </Canvas>
      <Svg>
        <AxisX formatTick="{(d) => format('.3%')(d)}" />
        <AxisY formatTick="{(d) => format(',')(d)}" />
        <Line x1="{0}" x2="{xMax}" y1="{r1}" y2="{r2}" />
      </Svg>
    </LayerCake>
  </div>
{/if}

<style>
  .chart {
    height: 50vh;
    width: 100%;
    padding: 0 4em;
    max-width: 80em;
    margin: 0 auto;
  }
</style>
