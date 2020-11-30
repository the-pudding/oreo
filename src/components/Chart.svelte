<script>
  import Popularity from "./charts/Popularity.svelte";
  import PopularityGrid from "./charts/PopularityGrid.svelte";
  import Frequency from "./charts/Frequency.svelte";
  import Clues from "./charts/Clues.svelte";
  import Time from "./charts/Time.svelte";
  import Scatter from "./charts/Scatter.svelte";
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

{#if name === 'time'}
  <Time />
{/if}

{#if name === 'scatter'}
  <Scatter />
{/if}
