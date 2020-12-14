<script>
  import { onMount } from "svelte";
  import { csv } from "d3-fetch";
  import { format } from "d3-format";
  import raw from "../../data/xd-oreo-clue-common-words-1993.csv";

  const words = raw.map((d) => ({ ...d, count: +d.count })).slice(0, 12);

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
    .slice(0, 10)
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
    <h3>Common Words</h3>
    <select bind:value="{active}">
      {#each words as { word, count }}
        <option value="{word}">
          <span class="word">{word}</span>
          <!-- <span class="count">{format(',')(count)}</span> -->
        </option>
      {/each}
    </select>
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
    <h3>Top 10 Examples (times used)</h3>
    <ul class="clues">
      {#each examples as { count, marked } (marked)}
        <li>
          <span class="clue">{@html marked}</span>
          <span class="count">({format(',')(count)})</span>
        </li>
      {/each}
    </ul>
  </div>
</div>

<style>
  .outer {
    display: flex;
    justify-content: center;
    flex-direction: column;
  }

  h3 {
    text-align: center;
    text-transform: uppercase;
    font-size: 0.75em;
    font-weight: var(--bold);
  }

  ul {
    margin: 0 0.5em;
    list-style-type: none;
  }

  .active button {
    background: var(--highlight);
  }

  .words {
    display: none;
    flex-wrap: wrap;
    width: 16.5em;
    justify-content: space-between;
  }

  .words li {
    padding: 0.5em;
  }

  .words button {
    display: flex;
    width: 7.25em;
    justify-content: space-between;
    align-items: baseline;
  }

  .words span {
    display: inline-block;
  }

  .word {
    margin-right: 0.5em;
    font-weight: var(--bold);
  }

  .words .count {
    display: inline-block;
    font-size: 0.75em;
  }

  .clues {
    width: 16.5em;
  }

  .clues li {
    padding-top: 0.5em;
    /* display: flex; */
    /* align-items: baseline; */
  }

  .clues .count {
    margin-left: 0.5em;
    opacity: 0.75;
    font-size: 0.75em;
  }

  .left h3 {
    display: none;
  }

  .left {
    display: flex;
    justify-content: center;
    margin-bottom: 1em;
  }

  @media only screen and (min-width: 640px) {
    .outer {
      flex-direction: row;
    }

    ul.words {
      display: flex;
    }

    select {
      display: none;
    }

    .left {
      display: block;
    }

    .left h3 {
      display: block;
    }
  }
</style>
