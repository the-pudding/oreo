<script>
  import raw from "../../data/xd-oreo-possible-1993.csv";
  import { scaleLinear } from "d3-scale";
  import { format } from "d3-format";

  const letters = [
    ["S", "O", "D", "A"],
    ["O", "V", "A", "L"],
    ["L", "E", "T", "S"],
    ["O", "R", "E", "O"],
  ];
  const scale = scaleLinear();
  let flipped = [false, false, false, false];

  const data = raw.map((d) => ({
    ...d,
    shareEven: +d.distributed_share_pct,
    shareOreo: +d.oreo_share_pct,
    mostUsed: d.most_used,
    mostLikely: d.most_likely,
    heatmap: d.heatmap.split("|").map((v) => +v),
    possible: +d.possible_anwers,
  }));

  const flip = (i) => {
    flipped[i] = !flipped[i];
    flipped = flipped;
  };

  $: query = letters[letters.length - 1]
    .map((d, i) => (flipped[i] ? d : "_"))
    .join("");
  $: datum = data.find((d) => d.query === query);
  // $: heatmap = datum.heatmap.map((d) => (d === datum.possible ? 0 : d));
  // $: query,
  //   scale.domain([
  //     Math.min(...datum.heatmap.filter((d) => d > 0)),
  //     Math.max(...datum.heatmap),
  //   ]);
</script>

<section>
  <div class="grid">
    {#each letters as ly, y}
      <div class="cards">
        {#each ly as letter, x}
          <div
            class="card"
            class:flip="{flipped[x]}"
            on:click="{() => flip(x)}">
            <div class="inner">
              <div class="front">
                <!-- <div class="bg" style="opacity: {scale(heatmap[x])};"></div> -->
                <span>?</span>
              </div>
              <div class="back"><span>{letter}</span></div>
            </div>
          </div>
        {/each}
      </div>
    {/each}
  </div>

  <div class="query">
    <p>
      <span class="prop">Query</span><span
        class="value">{datum.query ? datum.query
              .split('')
              .join(' ') : '&nbsp;'}</span>
    </p>
    <p>
      <span class="prop">Possible words</span><span
        class="value">{format(',')(datum.possible)}</span>
    </p>
    <p>
      <span class="prop">Even share</span><span
        class="value">{format('.2%')(datum.shareEven)}</span>
    </p>
    <p>
      <span class="prop">OREO share</span><span
        class="value">{format('.2%')(datum.shareOreo)}</span>
    </p>
    <p>
      <span class="prop">Most used</span><span
        class="value">{datum.mostUsed}</span>
    </p>
    <p>
      <span class="prop">Most probable</span><span
        class="value">{datum.mostLikely}</span>
    </p>
  </div>
</section>

<style>
  section {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .grid {
    display: flex;
    flex-direction: column;
    margin: 0 1em;
    /* width: 16em; */
  }
  .cards {
    display: flex;
    cursor: pointer;
    justify-content: center;
  }

  .cards:last-of-type .card .front {
    opacity: 1;
  }

  .cards:last-of-type .card .back {
    background: var(--fg);
    color: var(--bg);
    opacity: 1;
  }

  .card {
    position: relative;
    perspective: 1000px;
    width: 3em;
    height: 3em;
    border: 1px solid var(--bg);
  }

  .inner {
    position: relative;
    width: 100%;
    height: 100%;
    transform-style: preserve-3d;
    transition: transform 0.5s ease-in-out;
    transform-origin: 50% 50%;
  }

  .card.flip .inner {
    transform: rotateY(180deg);
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
    text-align: center;
    backface-visibility: hidden;
    z-index: 0;
    opacity: 0.5;
  }

  /* .bg {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: var(--highlight);
    z-index: 0;
    display: none;
  } */

  .front {
    background: white;
  }

  .back {
    background: var(--default);
    color: var(--bg);
    transform: rotateY(180deg);
  }

  .inner span {
    display: block;
    font-size: 2.5em;
    width: 100%;
    margin-top: 0.125em;
    position: relative;
  }

  .query {
    width: 12em;
    margin: 0 1em;
  }
  .query p {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    border-bottom: 1px dashed var(--default);
    font-size: 0.85em;
  }

  .query p:last-of-type {
    border: none;
  }

  .prop {
    text-transform: uppercase;
    font-size: 0.75em;
    font-weight: var(--bold);
  }
</style>
