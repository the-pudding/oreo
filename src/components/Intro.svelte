<script>
  import wordmark from "../svg/wordmark.svg";
  export let hed;
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

  <p style="margin-top: 2rem;">Arrow Key right.</p>
</section>

<style>
  section {
    margin: 0 auto;
    max-width: 50em;
  }
  .wordmark {
    max-width: 10em;
    margin: 1em auto;
  }
  h1 {
    font-size: 7vw;
    font-weight: var(--bold);
    line-height: 1;
  }
  .byline {
    margin-top: 1em;
    display: flex;
    /* justify-content: space-between; */
  }
  p {
    margin: 0;
    line-height: 1;
  }
</style>
