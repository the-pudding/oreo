<script>
  import wordmark from "../svg/wordmark.svg";
  import Icon from "./helpers/Icon.svelte";
  import ArrowKeys from "./ArrowKeys.svelte";
  export let hed;
  export let intro;
</script>

<section id="intro">
  <div class="top">
    <h1>{hed}</h1>

    <div class="byline">
      <div class="wordmark">
        <a href="https://pudding.cool">{@html wordmark}</a>
      </div>

      <p>
        <a href="https://pudding.cool/author/russell-goldenberg">Russell
          Goldenberg</a>
      </p>

      <time>January 2021</time>
    </div>
  </div>

  <h3><mark>{intro}</mark></h3>

  <div class="instructions">
    <p><span class="desktop">Use arrow keys or </span>tap below to navigate</p>
    <div class="keys">
      <ArrowKeys active="down" />
    </div>
  </div>

  <p class="next">
    Level 1
    <span>
      <Icon name="arrow-down" /></span>
  </p>
</section>

<style>
  section {
    margin: 0 auto;
    max-width: 70em;
    padding: 1rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin-top: var(--nav-height);
  }

  .wordmark {
    margin: 0 auto;
    width: 100%;
  }

  .top {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    display: flex;
    justify-content: space-between;
  }

  h1 {
    font-weight: var(--bold);
    line-height: 1;
    font-size: 1.25em;
    max-width: 12em;
    padding: 1rem;
    margin: 0;
    display: none;
  }

  h3 {
    font-size: 2em;
    /* text-align: center; */
  }

  mark {
    box-decoration-break: clone;
    /* padding: 0.2em; */
  }

  .byline {
    display: flex;
    flex-direction: column;
    font-size: 1em;
    padding: 0.5em 1em;
    padding-left: 1.5em;
    padding-top: 1.5em;
    max-width: 12em;
  }

  .byline p {
    margin: 0;
    line-height: 1;
    margin-bottom: 0.5em;
  }

  .instructions {
    text-transform: uppercase;
    margin-top: 2em;
    text-align: center;
  }

  .desktop {
    display: none;
  }

  .keys {
    display: flex;
    justify-content: center;
  }

  p.next {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    text-align: center;
    padding: 0.5em 0.75em;
    background-color: var(--fg);
    line-height: 1;
    margin: 0.1em;
    border-radius: 4px;
    font-size: 1em;
    display: flex;
    align-items: center;
    color: var(--off-white);
    text-transform: uppercase;
  }

  .next span {
    margin-left: 0.5em;
    display: flex;
    align-items: center;
  }

  .next {
    bottom: 1em;
  }

  @media only screen and (min-width: 640px) {
    h3 {
      font-size: 3em;
    }

    h1 {
      display: block;
      line-height: 1.4;
    }

    .byline {
      align-items: flex-end;
      padding: 0.5em 1em;
    }

    .desktop {
      display: inline;
    }
  }

  @media only screen and (min-width: 1200px) {
    h3 {
      font-size: 4em;
    }
  }
</style>
