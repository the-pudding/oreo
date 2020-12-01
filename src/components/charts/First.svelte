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
  console.log(years);
</script>

<div class="items">
  {#each years as { key, value }}
    <div class="item">
      <p class="leaf">
        {#each value as { words }}
          {#each words as word}<span>{word}</span>{/each}
        {/each}
      </p>
      <p class="stem">{key}</p>
    </div>
  {/each}
</div>

<style>
  .items {
    display: flex;
  }

  .item {
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
  }

  .stem {
    width: 5em;
  }

  p {
    margin: 0;
    text-align: center;
  }

  span {
    display: block;
    margin: 0;
    border: 1px solid var(--bg);
    line-height: 1;
    font-size: 0.625em;
    padding: 0.5em;
    background: var(--default);
    text-align: center;
    color: var(--bg);
  }
</style>
