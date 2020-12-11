<script>
  import { setContext, onMount } from "svelte";
  import { writable } from "svelte/store";
  import Slide from "./Slider.Slide.svelte";
  export let direction = "horizontal";
  export let active = 0;

  let width = 0;
  let height = 0;
  let translateEl;
  let children;

  let _direction = writable();
  let _width = writable();
  let _height = writable();

  $: w = direction === "horizontal" ? `${children * width}px` : "100%";
  $: h = direction === "vertical" ? `${children * height}px` : "100%";
  $: x = direction === "horizontal" ? `${active * width * -1}px` : 0;
  $: y = direction === "vertical" ? `${active * height * -1}px` : 0;

  // context
  $: $_direction = direction;
  $: $_width = `${width}px`;
  $: $_height = `${height}px`;
  $: context = { direction: _direction, width: _width, height: _height };
  $: setContext("Slider", context);

  onMount(() => {
    children = translateEl.children.length;
  });
</script>

<svelte:window bind:innerWidth="{width}" bind:innerHeight="{height}" />

<div class="slider {direction}">
  <div
    class="translate"
    bind:this="{translateEl}"
    style="width: {w}; height: {h}; transform: translate({x}, {y});">
    <slot />
  </div>
</div>

<style>
  .slider {
    position: relative;
    width: 100%;
    height: 100%;
    margin: 0;
    padding: 0;
    z-index: 1;
    overflow: hidden;
  }

  .translate {
    display: flex;
    position: relative;
    width: 100%;
    height: 100%;
    transition: transform 500ms ease-in-out;
    z-index: 1;
  }

  .horizontal .translate {
    flex-direction: row;
  }

  .vertical .translate {
    flex-direction: column;
  }
</style>
