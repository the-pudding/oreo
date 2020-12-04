<script>
  import Popularity from "./charts/Popularity.svelte";
  import PopularityGrid from "./charts/PopularityGrid.svelte";
  import Frequency from "./charts/Frequency.svelte";
  import Clues from "./charts/Clues.svelte";
  import CluesType from "./charts/CluesType.svelte";
  import Time from "./charts/Time.svelte";
  import Scatter from "./charts/Scatter.svelte";
  import Possible from "./charts/Possible.svelte";
  import First from "./charts/First.svelte";
  import Puzzle from "./charts/Puzzle.svelte";
  export let name;
</script>

{#if name === 'popularity'}
  <Popularity />
{/if}

{#if name === 'popularitygrid'}
  <PopularityGrid />
{/if}

{#if name === 'frequency'}
  <Frequency />
{/if}

{#if name === 'clues'}
  <Clues />
{/if}

{#if name === 'cluestype'}
  <CluesType />
{/if}

{#if name === 'time'}
  <Time />
{/if}

{#if name === 'scatter'}
  <Scatter />
{/if}

{#if name === 'possible'}
  <Possible />
{/if}

{#if name === 'first'}
  <First />
{/if}

{#if name === 'puzzle'}
  <Puzzle />
{/if}
