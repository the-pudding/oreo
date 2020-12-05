<script>
  import { onMount } from "svelte";
  import { LayerCake, Svg, Canvas } from "layercake";
  import { max, extent } from "d3-array";
  import { format } from "d3-format";
  import { scaleLinear, scalePow } from "d3-scale";
  import { line, curveStepBefore } from "d3-shape";
  import { axisLeft, axisBottom } from "d3-axis";
  import { csv } from "d3-fetch";
  import ScatterCanvas from "./Scatter.Canvas.svelte";

  const pad = 16;
  let data = [];
  let highlightData = [];
  let width = 1;
  let height = 1;
  let r = 4;
  let fill = "#187aaf";
  let canvas;
  let ctx;

  $: maxCount = max(data, (d) => d.count);
  $: maxProb = max(data, (d) => d.prob);
  $: xDomain = [0, maxProb];
  $: yDomain = [0, maxCount];
  $: height = width;
  $: scaleX = scalePow().exponent(0.5).domain(xDomain);

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

<div class="chart">
  <LayerCake
    padding="{{ top: 10, right: 10, bottom: 20, left: 20 }}"
    x="{'count'}"
    y="{'prob'}"
    xDomain="{xDomain}"
    yDomain="{yDomain}"
    yPadding="{[10, 10]}"
    data="{data}">
    <Canvas>
      <ScatterCanvas />
    </Canvas>
    <!-- <Svg>
      <AxisX />
      <AxisY
        formatTick="{(d) => format('.2%')(d)}"
        label="{' share of all clues'}" />
      <Line />
    </Svg> -->
  </LayerCake>
</div>

<style>
  .chart {
    height: 50vh;
    padding: 0 4em;
    max-width: 80em;
    margin: 0 auto;
  }
</style>
