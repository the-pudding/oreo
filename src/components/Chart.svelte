<script>
  import Popularity from "./charts/Popularity.svelte";
  import Frequency from "./charts/Frequency.svelte";
  export let name;
</script>

{#if name === 'popularity'}
  <Popularity />
{/if}

{#if name === 'frequency'}
  <Frequency />
{/if}
