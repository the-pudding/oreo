<script>
  import { createEventDispatcher } from "svelte";
  export let version;
  export let slides;
  export let index;

  const dispatch = createEventDispatcher();

  const onClick = () => {
    dispatch("jump", index);
  };
</script>

<button class="{version}" on:click="{onClick}">
  <span class="title">{version}</span>
  <div class="cookie top"></div>
  <div class="progress">
    {#each slides as slide}<span class="unit"></span>{/each}
  </div>

  <div class="cookie bottom"></div>
</button>

<style>
  button {
    background: none;
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 6em;
  }
  .title {
    margin-bottom: 0.5em;
    text-transform: capitalize;
  }
  .progress {
    width: 2.5em;
  }
  .unit {
    height: 3px;
    display: block;
    background: var(--gray-light);
  }
  .cookie {
    width: 3em;
    height: 0.25em;
    background: var(--off-black);
    border-radius: 2px;
  }
</style>
