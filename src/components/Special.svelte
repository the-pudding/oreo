<script>
  import Recirc from "./special/Recirc.svelte";
  import Clue from "./special/Clue.svelte";
  import Commercial from "./special/Commercial.svelte";
  import Mukbang from "./special/Mukbang.svelte";
  import Antelope from "./special/Antelope.svelte";
  import Puzzle from "./special/Puzzle.svelte";
  export let name;
</script>

{#if name === 'recirc'}
  <Recirc />
{/if}

{#if name === 'clue'}
  <Clue />
{/if}

{#if name === 'commercial'}
  <Commercial />
{/if}

{#if name === 'mukbang'}
  <Mukbang />
{/if}

{#if name === 'antelope'}
  <Antelope />
{/if}

{#if name === 'puzzle'}
  <Puzzle />
{/if}
