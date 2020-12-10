<script>
  import Crossword from "svelte-crossword";
  import data from "./puzzle.json";
</script>

<section>
  <Crossword data="{data}" />
</section>

<style>
  section {
    max-width: 35em;
    margin: 0 auto;
  }
</style>
