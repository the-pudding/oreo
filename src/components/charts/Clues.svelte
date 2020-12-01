<script>
  import { onMount } from "svelte";
  import { csv } from "d3-fetch";
  import { format } from "d3-format";
  import raw from "../../data/xd-oreo-clue-common-words-1993.csv";

  const min = 100;

  const words = raw
    .map((d) => ({ ...d, count: +d.count }))
    .filter((d) => d.count >= min);

  let clues = [];
  let active = words[0].word;

  const addMark = (str) => {
    const start = str.toLowerCase().indexOf(active);
    const end = start + active.length;
    const before = str.substring(0, start);
    const tween = str.substring(start, end);
    const after = str.substring(end, str.length);
    return `${before}<mark>${tween}</mark>${after}`;
  };

  $: examples = clues
    .filter((d) => d.clue.toLowerCase().includes(active))
    .slice(0, 20)
    .map((d) => ({
      ...d,
      marked: addMark(d.clue),
    }));

  const cleanClues = (arr) => {
    return arr.map((d) => ({
      ...d,
      count: +d.count,
      percent: +d.percent,
    }));
  };

  onMount(() => {
    csv("assets/data/xd-oreo-clues-freq-1993.csv")
      .then(cleanClues)
      .then((result) => (clues = result))
      .catch((err) => {
        console.log(err);
      });
  });
</script>

<div class="outer">
  <div class="left">
    <h3>Word Count</h3>
    <ul class="words">
      {#each words as { word, count }}
        <li class:active="{active === word}">
          <button on:click="{() => (active = word)}">
            <span class="word">{word}</span>
            <span class="count">{format(',')(count)}</span>
          </button>
        </li>
      {/each}
    </ul>
  </div>

  <div class="right">
    <h3>Examples</h3>
    <ul class="clues">
      {#each examples as { count, marked } (marked)}
        <li>
          {@html marked}
        </li>
      {/each}
    </ul>
  </div>
</div>

<style>
  .outer {
    display: flex;
    justify-content: center;
  }

  ul {
    margin: 0 1em;
    list-style-type: none;
  }

  .active button {
    background: var(--highlight);
  }

  .words {
    width: 15em;
  }

  .words li {
    margin-bottom: 0.5em;
  }

  .words span {
    display: inline-block;
  }

  .word {
    margin-right: 0.5em;
    width: 5em;
    text-align: left;
  }

  .count {
    width: 3em;
  }

  .clues {
    width: 15em;
  }

  .clues li {
    margin-bottom: 0.5em;
  }
</style>
