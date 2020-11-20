<script>
  import Recirc from "./special/Recirc.svelte";
  export let name;
</script>

{#if name === 'recirc'}
  <Recirc />
{/if}
