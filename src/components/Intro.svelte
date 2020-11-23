<script>
  import wordmark from "../svg/wordmark.svg";
  import Icon from "./helpers/Icon.svelte";
  export let hed;
  export let intro;
</script>

<section id="intro">
  <div class="wordmark">
    <a href="https://pudding.cool">{@html wordmark}</a>
  </div>

  <h1>{hed}</h1>

  <div class="byline">
    <time>December 2020</time>
    &nbsp;|&nbsp;
    <p>
      <a href="https://pudding.cool/author/russell-goldenberg">Russell
        Goldenberg</a>
    </p>
  </div>

  <h3>{intro}</h3>

  <p style="margin-top: 2rem;">Arrow Key right.</p>
  <button><Icon name="triangle" direction="e" /></button>
</section>

<style>
  section {
    margin: 0 auto;
    max-width: 50em;
    padding: 1rem;
  }

  .wordmark {
    max-width: 10em;
    margin: 1em auto;
  }

  h1 {
    font-weight: var(--bold);
    line-height: 1;
    font-size: 1.5em;
  }

  h3 {
    font-size: 6vh;
  }

  .byline {
    display: flex;
    font-size: 2vh;
    align-items: center;
  }

  .byline p {
    margin: 0;
    line-height: 1;
  }

  button {
    font-size: 2em;
    background: none;
    color: var(--fg);
  }
</style>
