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

  let value = years[0].key;
  $: active = +value;
  $: terms = years.find((d) => d.key === active).value;
  $: console.log(terms);
</script>

<div class="mini">
  <div class="items">
    {#each years as { key, value }}
      <div class="item" class:active="{key === active}">
        <div class="leaf">
          {#each value as { words }}
            {#each words as word}
              <p class="word"></p>
            {/each}
          {/each}
        </div>
        <p class="stem" class:visible="{key === active}">{key}</p>
      </div>
    {/each}
  </div>
</div>

<div class="slider">
  <input bind:value type="range" min="1993" max="2020" />
</div>

<div class="outer">
  <div class="terms">
    {#each terms as { words, clue }}
      {#each words as word}
        <div class="term">
          <p class="text">{word}</p>
          <p class="clue">{clue}</p>
        </div>
      {/each}
    {/each}
  </div>
</div>

<style>
  .outer {
    max-width: 60em;
    margin: 0 auto;
  }

  .slider {
    display: flex;
    justify-content: center;
    margin: 1.25em auto;
    width: 15em;
  }

  input {
    width: 100%;
  }

  .mini {
  }

  .items {
    display: flex;
    max-width: 15em;
    margin: 0 auto;
  }

  .item {
    position: relative;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    flex-grow: 1;
    transition: all 0ms ease-in-out;
  }

  .stem {
    margin: 0;
    font-size: 0.75em;
    white-space: nowrap;
    position: absolute;
    bottom: 0;
    left: 50%;
    transform: translate(-50%, 100%);
    display: none;
    font-weight: var(--bold);
    /* margin-top: 1em; */
  }

  .stem.visible {
    display: block;
  }

  .leaf {
    margin: 0;
    text-align: center;
  }

  .word {
    display: block;
    margin: 0;
    /* border: 0.5px solid var(--bg); */
    box-shadow: 0 0 1px 0 var(--default);
    line-height: 1;
    background: var(--default);
    font-weight: var(--bold);
    height: 0.25em;
    width: 100%;
    /* width: 1em;
    height: 1em; */
  }

  /* .word:hover {
    transform: scale(2);
  } */

  span {
    /* display: inline-block; */
    white-space: nowrap;
    visibility: hidden;
  }
  /* 
  .item.active {
    width: 6em;
  }
*/
  .active .word {
    background: var(--highlight);
  }

  .terms {
    display: flex;
    flex-wrap: wrap;
    height: 40vh;
    align-items: flex-start;
    align-content: flex-start;
    justify-content: center;
  }

  .term {
    position: relative;
    display: flex;
    flex-direction: column;
    justify-content: center;
    position: relative;
    box-shadow: 0 0 1px 0 var(--fg);
    margin: 1px;
    background: var(--highlight);
    width: 12em;
    height: 5em;
    font-size: 0.625em;
    border-radius: 4px;
    text-align: center;
    font-weight: var(--bold);
    margin: 0;
    cursor: pointer;
  }

  .clue {
    display: none;
    position: absolute;
    pointer-events: none;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: var(--fg);
    color: var(--bg);
    margin: 0;
    align-items: center;
    justify-content: center;
    padding: 0.5em;
    line-height: 1.2;
  }

  .text {
    margin: 0;
  }

  .term:hover .clue {
    display: block;
    display: flex;
  }
</style>
