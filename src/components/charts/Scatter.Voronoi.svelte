<script>
  import { Delaunay } from "d3-delaunay";
  import { extent } from "d3-array";
  import { getContext } from "svelte";
  import { uniques } from "layercake";

  const { data, xGet, yGet, width, height } = getContext("LayerCake");
  const yThreshold = 32;
  const xThreshold = 32;

  const bigEnough = (point, i) => {
    const cell = voronoi.cellPolygon(i);
    if (!cell) return false;
    const [cx, cy] = point;
    const [ax, bx] = extent(cell.map(([x, y]) => x));
    const [ay, by] = extent(cell.map(([x, y]) => y));
    const w = bx - ax;
    const h = by - ay;
    const dx1 = cx - ax;
    const dx2 = bx - cx;
    const dy1 = cy - ay;
    const dy2 = by - cy;
    const label =
      dx1 > xThreshold &&
      dx2 > xThreshold &&
      dy1 > yThreshold &&
      dy2 > yThreshold;
    const big = w > xThreshold * 3 && h > yThreshold * 3;
    return label || big;
  };

  $: points = $data
    .filter((d) => d.prob > 0.00004 || d.count > 1000)
    .map((d) => {
      const point = [$xGet(d), $yGet(d)];
      point.data = d;
      return point;
    });

  $: uniquePoints = uniques(points, (d) => d.join(), false);

  $: voronoi = Delaunay.from(points).voronoi([0, 0, $width, $height]);
</script>

{#each uniquePoints as point, i}
  {#if bigEnough(point, i)}
    <!-- <path
      class="voronoi-cell"
      d="{voronoi.renderCell(i)}"
      }"></path> -->
    <text
      class:oreo="{point.data.answer === 'OREO'}"
      text-anchor="middle"
      x="{point[0]}"
      y="{point[1]}"
      dy="{point.data.answer === 'OREO' ? -12 : -6}">
      {point.data.answer}
    </text>
  {/if}
{/each}

<style>
  text {
    font-size: 12px;
  }

  .oreo {
    font-weight: var(--bold);
    font-size: 16px;
  }
</style>
