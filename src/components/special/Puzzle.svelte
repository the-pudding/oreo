<script>
  import { onMount } from "svelte";
  import Crossword from "svelte-crossword";
  import data from "./puzzle.json";

  let mounted;

  onMount(() => {
    mounted = true;
  });
</script>

<section>
  {#if mounted}
    <Crossword data="{data}" />
  {/if}
</section>

<style>
  section {
    width: 100%;
    max-width: 35em;
    margin: 0 auto;
  }
</style>
