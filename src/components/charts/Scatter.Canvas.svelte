<script>
  import { getContext } from "svelte";
  import { scaleCanvas } from "layercake";
  const { data, xGet, yGet, width, height } = getContext("LayerCake");
  const { ctx } = getContext("canvas");
  export let r = 1;
  export let fill = "#000";

  $: {
    if ($ctx) {
      scaleCanvas($ctx, $width, $height);
      $ctx.clearRect(0, 0, $width, $height);

      $data.forEach((d, i) => {
        const mult = d.answer === "OREO" ? 3 : 1;
        const f = d.answer === "OREO" ? "#0c3f5a" : fill;
        if (d.answer === "OREO") {
          $ctx.beginPath();
          $ctx.arc($xGet(d), $yGet(d), r * mult * 1.5, 0, 2 * Math.PI, false);
          $ctx.fillStyle = "#e8e500";
          $ctx.fill();
        }
        $ctx.beginPath();
        $ctx.arc($xGet(d), $yGet(d), r * mult, 0, 2 * Math.PI, false);
        $ctx.fillStyle = f;
        $ctx.fill();
      });
    }
  }
</script>
