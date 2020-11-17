<script>
  import Nice from "./charts/Nice.svelte";
  export let chart;
</script>

{#if chart === 'nice'}
  <Nice />
{/if}
