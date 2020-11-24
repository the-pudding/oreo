<script>
  import Popularity from "./charts/Popularity.svelte";
  import Frequency from "./charts/Frequency.svelte";
  import Clues from "./charts/Clues.svelte";
  export let name;
</script>

{#if name === 'popularity'}
  <Popularity />
{/if}

{#if name === 'frequency'}
  <Frequency />
{/if}

{#if name === 'clues'}
  <Clues />
{/if}
