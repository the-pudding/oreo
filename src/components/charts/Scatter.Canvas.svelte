<script>
  import { getContext } from "svelte";
  const { data, xGet, yGet, yScale, xScale } = getContext("LayerCake");
  const { ctx } = getContext("canvas");

  $: if ($ctx) {
    $ctx.clearRect(0, 0, width, height);

    data.forEach((d) => {
      $ctx.beginPath();
      $ctx.arc(
        scaleX(d.prob) * 2,
        scaleY(d.count) * 2,
        r,
        0,
        2 * Math.PI,
        false
      );
      $ctx.fillStyle = fill;
      $ctx.fill();
    });
  }
</script>
