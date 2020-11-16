<script>
  import wordmark from "../svg/wordmark.svg";
</script>

<header>
  <div class="wordmark">
    <a
      href="https://pudding.cool"
      target="_blank"
      rel="noopener">{@html wordmark}</a>
  </div>
</header>

<style>
  header {
    width: 100%;
    top: 0;
    left: 0;
    position: fixed;
    z-index: 1000;
  }
  .wordmark {
    max-width: 10em;
    margin: 1em auto;
  }
</style>
