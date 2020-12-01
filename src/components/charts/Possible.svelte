<script>
  import raw from "../../data/xd-oreo-possible-1993.csv";
  import { scaleLinear } from "d3-scale";

  const letters = ["O", "R", "E", "O"];
  const scale = scaleLinear();
  let flipped = [false, false, false, false];

  const data = raw.map((d) => ({
    ...d,
    shareEven: +d.distributed_share_pct,
    shareOreo: +d.oreo_share_pct,
    heatmap: d.heatmap.split("|").map((v) => +v),
    possible: +d.possible_anwers,
  }));

  const flip = (i) => {
    flipped[i] = !flipped[i];
    flipped = flipped;
  };

  $: query = letters.map((d, i) => (flipped[i] ? d : "_")).join("");
  $: datum = data.find((d) => d.query === query);
  $: heatmap = datum.heatmap.map((d) => (d === datum.possible ? 0 : d));
  $: query,
    scale.domain([
      Math.min(...datum.heatmap.filter((d) => d > 0)),
      Math.max(...datum.heatmap),
    ]);
</script>

<div class="cards">
  {#each letters as letter, i}
    <div class="card" class:flip="{flipped[i]}" on:click="{() => flip(i)}">
      <div class="inner">
        <div class="front">
          <div class="bg" style="opacity: {scale(heatmap[i])};"></div>
          <span>?</span>
        </div>
        <div class="back"><span>{letter}</span></div>
      </div>
    </div>
  {/each}
</div>

<style>
  .cards {
    display: flex;
    cursor: pointer;
    justify-content: center;
  }

  .card {
    perspective: 1000px;
  }

  .flip .inner {
    transform: rotateY(180deg);
  }

  .card,
  .inner {
    position: relative;
    width: 5em;
    height: 5em;
  }

  .inner {
    transition: transform 0.5s ease-in-out;
    transform-origin: 50% 50%;
    transform-style: preserve-3d;
  }

  .front,
  .back {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    backface-visibility: hidden;
    text-align: center;
  }

  .bg {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: var(--highlight);
    z-index: 0;
  }

  .front {
    /* background: white; */
  }

  .back {
    background: var(--default);
    color: var(--bg);
    transform: rotateY(180deg);
  }

  span {
    display: block;
    font-size: 4em;
    width: 100%;
    margin-top: 0.125em;
    position: relative;
  }
</style>
