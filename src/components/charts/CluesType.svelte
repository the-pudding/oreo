<script>
  import { onMount } from "svelte";
  import { csv } from "d3-fetch";
  import { format } from "d3-format";
  import { scaleLinear } from "d3-scale";
  import { distance } from "fastest-levenshtein";
  import raw from "../../data/xd-oreo-clue-common-words-1993.csv";

  const min = 100;

  const words = raw
    .map((d) => ({ ...d, count: +d.count }))
    .filter((d) => d.count >= min);

  let guess = "";
  let clues = [];
  let active = words[0].word;
  let reveal;

  const getGrams = (str) => {
    return str
      .toLowerCase()
      .replace(/[^a-z]/g, " ")
      .split(" ")
      .map((d) => d.trim())
      .filter((d) => d);
  };

  const compareGrams = (a, b) => {
    if (a.length < b.length) {
      const matches = a.filter((d) => b.includes(d)).length;
      return matches / b.length;
    }

    const matches = b.filter((d) => a.includes(d)).length;
    return matches / a.length;
  };

  const onSubmit = (e) => {
    e.preventDefault();
    const temp = clues.map((d) => ({
      ...d,
      scoreLev: distance(guess.toLowerCase(), d.lower),
      scoreGram: compareGrams(guessGrams, d.grams),
    }));
    const lev = temp.map((d) => d.scoreLev);
    const gram = temp.map((d) => d.scoreGram);

    const minLev = Math.min(...lev);
    const maxLev = Math.max(...lev);

    const minGram = Math.min(...gram);
    const maxGram = Math.max(...gram);

    const scaleLev = scaleLinear().domain([minLev, maxLev]);
    const scaleGram = scaleLinear().domain([maxGram, minGram]);

    const rank = temp.map((d) => ({
      ...d,
      score: scaleLev(d.scoreLev) + scaleGram(d.scoreGram),
    }));
    rank.sort((a, b) => a.score - b.score);
    clues = rank;
    reveal = true;
  };

  const addMark = (str) => {
    const start = str.toLowerCase().indexOf(active);
    const end = start + active.length;
    const before = str.substring(0, start);
    const tween = str.substring(start, end);
    const after = str.substring(end, str.length);
    return `${before}<mark>${tween}</mark>${after}`;
  };

  const cleanClues = (arr) => {
    return arr.map((d) => ({
      ...d,
      lower: d.clue.toLowerCase(),
      grams: getGrams(d.clue),
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

  $: maxLength = clues ? Math.max(...clues.map((d) => d.clue.length)) : 0;
  $: examples = clues
    .filter((d) => d.clue.toLowerCase().includes(active))
    .slice(0, 20)
    .map((d) => ({
      ...d,
      marked: addMark(d.clue),
    }));
  $: guessGrams = getGrams(guess);
  $: top = clues.slice(0, 10);
</script>

<fieldset>
  <label for="clue">How would you clue OREO?</label>
  <input
    bind:value="{guess}"
    name="clue"
    placeholder="Clue description"
    maxlength="{maxLength}" />
  <button on:click="{onSubmit}">Submit</button>
</fieldset>

{#if reveal}
  {#each top as { clue }}
    <p>{clue}</p>
  {/each}
{/if}

<style>
  fieldset {
    outline: none;
    border: none;
    margin: 0;
    padding: 0;
  }

  input {
    width: 100%;
  }
</style>
