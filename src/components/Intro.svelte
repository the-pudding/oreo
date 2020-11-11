<script>
  import Slider from "./Slider.svelte";
</script>

<section id="intro">
  <h1>Oreos and the Art of Crossword Puzzle Construction</h1>
  <div>
    <time>November 2020</time>
    &nbsp;|&nbsp;
    <p>
      <a
        href="https://pudding.cool/author/russell-goldenberg"
        target="_blank"
        rel="noopener">Russell Goldenberg</a>
    </p>
  </div>

  <Slider />
</section>

<style>
  section {
    margin: 0 auto;
    max-width: 50em;
  }
  h1 {
    font-size: 5em;
    font-weight: var(--bold);
    line-height: 1;
  }
  div {
    margin-top: 1em;
    display: flex;
    /* justify-content: space-between; */
  }
  p {
    margin: 0;
    line-height: 1;
  }
  time {
    /* text-align: right; */
  }
</style>
