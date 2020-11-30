<script>
  import { format } from "d3-format";
  import { scaleLinear } from "d3-scale";
  import { line, curveStepBefore } from "d3-shape";
  import data from "../../data/xd-nyt-oreo-1950.csv";

  const cleanData = data
    .map((d) => ({
      ...d,
      year: +d.year,
      four: +d.four,
      cookie: +d.cookie,
      mountain: +d.mountain,
    }))
    .map((d) => ({
      ...d,
      pctCookie: d.cookie / d.four,
      pctMountain: d.mountain / d.four,
    }));

  const minYear = Math.min(...cleanData.map((d) => d.year));
  const maxYear = Math.max(...cleanData.map((d) => d.year));
  const domainX = [minYear, maxYear];
  const maxCookie = Math.max(...cleanData.map((d) => d.pctCookie));
  const maxMountain = Math.max(...cleanData.map((d) => d.pctMountain));
  const domainY = [0, Math.max(maxCookie, maxMountain)];

  let width = 1;
  let height = 1;
  let pad = 4;

  $: height = Math.floor(width / 2);
  $: scaleX = scaleLinear()
    .domain(domainX)
    .range([0, width - pad * 2]);
  $: scaleY = scaleLinear()
    .domain(domainY)
    .range([height - pad * 2, 0]);
  // $: pathC =
  //   "M" +
  //   cleanData.map((d) => `${scaleX(d.year)},${scaleY(d.pctCookie)}`).join("L");
  // $: pathM =
  //   "M" +
  //   cleanData
  //     .map((d) => `${scaleX(d.year)},${scaleY(d.pctMountain)}`)
  //     .join("L");
  $: pathC = line()
    .x((d) => scaleX(d.year))
    .y((d) => scaleY(d.pctCookie))
    .curve(curveStepBefore)(cleanData);
  $: pathM = line()
    .x((d) => scaleX(d.year))
    .y((d) => scaleY(d.pctMountain))
    .curve(curveStepBefore)(cleanData);
</script>

<div bind:offsetWidth="{width}">
  <svg width="{width}" height="{height}">
    <g transform="translate({pad}, {pad})">
      <path class="mountain" d="{pathM}"></path>
      <path class="cookie" d="{pathC}"></path>
    </g>
  </svg>
</div>

<style>
  svg {
    display: block;
  }

  path {
    fill: none;
    stroke-width: 2px;
  }

  .cookie {
    stroke: var(--primary);
  }

  .mountain {
    stroke: var(--default);
  }
</style>
