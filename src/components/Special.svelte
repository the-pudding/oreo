<script>
  import Recirc from "./special/Recirc.svelte";
  import Clue from "./special/Clue.svelte";
  export let name;
</script>

{#if name === 'recirc'}
  <Recirc />
{/if}

{#if name === 'clue'}
  <Clue />
{/if}
