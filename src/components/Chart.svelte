<script>
  import Nice from "./charts/Nice.svelte";
  export let name;

  const loadedData = [
    { x: 5, y: 20 },
    { x: 100, y: 100 },
  ];
</script>

{#if name === 'nice'}
  <Nice data="{loadedData}" />
  <Nice />
{/if}
