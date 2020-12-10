<script>
  import { scaleLinear, scalePow } from "d3-scale";
  let terms = [
    { name: "ELAND", count: 162 },
    { name: "GNU", count: 99 },
    { name: "ORIBI", count: 65 },
    { name: "IMPALA", count: 37 },
    { name: "TOPI", count: 32 },
    { name: "KUDU", count: 25 },
    { name: "NYALA", count: 21 },
    { name: "TORA", count: 15 },
    { name: "DIKDIK", count: 6 },
    { name: "SUNI", count: 5 },
    { name: "ADDAX", count: 5 },
    { name: "BONGO", count: 4 },
    { name: "KOB", count: 3 },
    { name: "ASSE", count: 3 },
    { name: "ETAAC", count: 3 },
    { name: "RHEBOK", count: 3 },
    { name: "GEMSBOK", count: 3 },
    { name: "STEENBOK", count: 3 },
    { name: "TIANG", count: 1 },
    { name: "BLESBOK", count: 1 },
    { name: "SASSABY", count: 1 },
    { name: "GERENUK", count: 1 },
    { name: "REITBOK", count: 1 },
    { name: "DUIKER", count: 1 },
    { name: "SITATUNGA", count: 1 },
    { name: "KLIPSPRINGER", count: 1 },
  ];

  let guess = "";

  const max = Math.max(...terms.map((d) => d.count));
  // $: scale = scaleLinear().domain([0, max]).range([0, 100]);
  $: scale = scalePow().exponent(0.5).domain([0, max]).range([0, 100]);
  $: upper = guess.toUpperCase();

  const onSubmit = (e) => {
    e.preventDefault();
    const match = terms.find((d) => d.name === upper);
    match.correct = true;
    terms = terms;
    guess = "";
  };

  const onReveal = (e) => {
    e.preventDefault();
    terms.forEach((t) => (t.correct = true));
    terms = terms;
  };
</script>

<section>
  <fieldset>
    <label for="clue">Name an African antelope</label>
    <input bind:value="{guess}" name="clue" placeholder="Enter name..." />
    <button on:click="{onSubmit}">Submit</button>
  </fieldset>
  <p><button on:click="{onReveal}">Reveal Answers</button></p>
</section>
<div class="outer">
  <div class="terms">
    {#each terms as { name, count, correct }}
      <div class="term">
        <span class="bg" style="opacity: {scale(count)}%;"></span>
        <span class="name">{correct ? name : '?'}</span>
        <span class="count">{count}</span>
      </div>
    {/each}
  </div>
</div>

<style>
  .outer {
    max-width: 60em;
    margin: 0 auto;
  }

  section {
    max-width: 20em;
    margin: 0 auto;
  }

  fieldset {
    width: 100%;
    outline: none;
    border: none;
    margin: 0 auto;
    padding: 0;
    display: flex;
    flex-wrap: wrap;
  }

  label {
    display: block;
    width: 100%;
  }

  input {
    flex-grow: 2;
    font-size: 0.75em;
  }

  fieldset button {
    margin-left: 1em;
    font-weight: var(--bold);
  }

  p button {
    font-size: 0.75em;
    font-weight: var(--bold);
  }

  .terms {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }

  span {
    display: block;
    text-align: center;
    color: var(--fg);
    position: relative;
    line-height: 1;
    width: 100%;
  }

  .bg {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: var(--highlight);
  }

  .term {
    padding: 0.5em;
    position: relative;
    display: flex;
    flex-direction: column;
    justify-content: center;
    position: relative;
    box-shadow: 0 0 1px 0 var(--fg);
    margin: 1px;
    width: 8.5em;
    font-size: 0.75em;
    border-radius: 4px;
    text-align: center;
    margin: 0;
  }

  .name {
    font-weight: var(--bold);
  }

  .count {
    margin-top: 0.5em;
    font-size: 0.8em;
  }

  .correct {
  }
</style>
