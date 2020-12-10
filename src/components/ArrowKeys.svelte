<script>
  import Icon from "./helpers/Icon.svelte";
  export let active;
</script>

<div>
  <span></span>
  <span class:active="{active === 'up'}"><Icon name="arrow-up" /></span>
  <span></span>
  <span class:active="{active === 'left'}"><Icon name="arrow-left" /></span>
  <span class:active="{active === 'down'}"><Icon name="arrow-down" /></span>
  <span class:active="{active === 'right'}"><Icon name="arrow-right" /></span>
</div>

<style>
  div {
    display: grid;
    grid: repeat(2, 1fr) / repeat(3, 1fr);
    font-size: 1rem;
    width: 5em;
  }

  span {
    display: flex;
    align-items: center;
    padding: 0.25em;
    background-color: var(--fg);
    color: var(--off-white);
    line-height: 1;
    margin: 0.1em;
    border-radius: 4px;
    opacity: 0.3;
  }

  span:empty {
    opacity: 0;
  }

  span.active {
    opacity: 1;
  }
</style>
