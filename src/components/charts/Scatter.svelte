<script>
  import { onMount } from "svelte";
  import { format } from "d3-format";
  import { scaleLinear, scalePow } from "d3-scale";
  import { line, curveStepBefore } from "d3-shape";
  import { axisLeft, axisBottom } from "d3-axis";
  import { csv } from "d3-fetch";

  const pad = 16;
  let data = [];
  let highlightData = [];
  let width = 1;
  let height = 1;
  let r = 4;
  let fill = "#187aaf";
  let canvas;
  let ctx;

  $: maxCount = Math.max(...data.map((d) => d.count));
  $: maxProb = Math.max(...data.map((d) => d.prob));
  $: domainX = [0, maxProb];
  $: domainY = [0, maxCount];
  $: height = width;
  $: scaleX = scalePow()
    .exponent(0.5)
    .domain(domainX)
    .range([pad * 2, width - pad * 2]);
  $: scaleY = scaleLinear()
    .domain(domainY)
    .range([height - pad * 2, pad * 2]);

  $: axisX = axisBottom(scaleX)();
  $: axisY = axisLeft(scaleY)();

  $: console.log(axisY);

  $: if (ctx && data) {
    ctx.clearRect(0, 0, width, height);

    data.forEach((d) => {
      ctx.beginPath();
      ctx.arc(
        scaleX(d.prob) * 2,
        scaleY(d.count) * 2,
        r,
        0,
        2 * Math.PI,
        false
      );
      ctx.fillStyle = fill;
      ctx.fill();
    });
  }

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
    ctx = canvas.getContext("2d");
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

<div bind:offsetWidth="{width}" style="height: {height}px;">
  <canvas
    bind:this="{canvas}"
    width="{width * 2}"
    height="{height * 2}"
    style="width: {width}px; height: {height}px;"></canvas>
  <svg width="{width}" height="{height}">
    <g transform="translate({pad}, {pad})">
      {#each highlightData as { answer, prob, count }}
        <g
          class:highlight="{answer === 'OREO'}"
          class:visible="{answer === 'OREO'}"
          transform="translate({scaleX(prob)}, {scaleY(count)})">
          <text
            class="bg"
            y="-8"
            alignment-baseline="baseline"
            text-anchor="middle">
            {answer}
          </text>
          <text
            class="fg"
            y="-8"
            alignment-baseline="baseline"
            text-anchor="middle">
            {answer}
          </text>
          <circle cx="0" cy="0" r="{r}"></circle>
        </g>
      {/each}
    </g>
  </svg>
</div>

<style>
  div {
    position: relative;
  }

  circle {
    fill: var(--primary);
  }

  text {
    fill: var(--primary);
    font-weight: var(--bold);
  }

  text.bg {
    stroke: var(--bg);
    stroke-width: 4px;
    fill: none;
  }

  svg {
    position: absolute;
    top: 0;
    left: 0;
  }

  canvas {
    position: absolute;
    top: 0;
    left: 0;
  }
</style>
