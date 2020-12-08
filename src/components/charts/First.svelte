<script>
  import { group } from "d3-array";
  import mapToArray from "../../utils/mapToArray.js";
  import raw from "../../data/xd-nyt-firsts-1993.csv";
  const data = raw.map((d) => ({
    ...d,
    words: d.words.split(","),
    year: +d.year,
  }));

  const years = mapToArray(group(data, (d) => d.year));

  let w = 1;
  let itemW = 1;
  $: itemsWidth = years.length * itemW;
</script>

<div class="slider"><input type="range" min="1993" max="2020" /></div>

<div class="outer">
  <div class="items" bind:clientHeight="{w}">
    {#each years as { key, value }}
      <div class="item" bind:clientWidth="{itemW}">
        <div class="leaf">
          {#each value as { words }}
            {#each words as word}
              <p class="word"><span>{word}</span></p>
            {/each}
          {/each}
        </div>
        <p class="stem">{key}</p>
      </div>
    {/each}
  </div>
</div>

<style>
  .slider {
    display: flex;
    justify-content: center;
    margin-bottom: 1em;
  }
  .items {
    display: flex;
    width: auto;
  }

  .item {
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    min-width: 5em;
  }

  .stem {
    margin: 0;
    font-size: 0.75em;
    /* transform: rotate(45deg); */
    /* width: 3em; */
    text-align: center;
    /* margin-top: 1em; */
  }

  .leaf {
    margin: 0;
    text-align: center;
  }

  .word {
    display: block;
    margin: 0;
    border: 1px solid var(--bg);
    line-height: 1;
    font-size: 0.5em;
    padding: 0.5em;
    background: var(--default);
    text-align: center;
    color: var(--bg);
    font-weight: var(--bold);
    /* width: 1em;
    height: 1em; */
  }

  .word:hover {
    transform: scale(2);
  }

  span {
    display: inline-block;
    white-space: nowrap;
    /* display: none; */
  }
</style>
