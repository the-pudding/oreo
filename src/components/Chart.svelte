<script>
  import Popularity from "./charts/Popularity.svelte";
  export let name;
</script>

{#if name === 'popularity'}
  <Popularity />
{/if}
