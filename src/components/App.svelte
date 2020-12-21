<script>
  import { onMount } from "svelte";
  import Meta from "./Meta.svelte";
  import Header from "./Header.svelte";
  import Nav from "./Nav.svelte";
  import Intro from "./Intro.svelte";
  import Slides from "./Slides.svelte";
  import Tap from "./helpers/Tap.svelte";
  import Slider from "./helpers/Slider.svelte";
  import Slide from "./helpers/Slider.Slide.svelte";

  import { visibleIndex } from "../stores/nav.js";
  import copy from "../data/copy.json";
  let innerWidth;
  let innerHeight;

  let sliderY;
  let activeY;
  let countY;

  let sliderX = [];
  let activeX = [];
  let countX = [];

  let currentX = 0;

  const onTap = ({ detail }) => {
    if (detail === "left") sliderX.forEach((s) => s.prev());
    else if (detail === "right") sliderX.forEach((s) => s.next());
    else if (detail === "up") sliderY.prev();
    else if (detail === "down") sliderY.next();
  };

  const updateArrows = () => {
    currentX = activeX[activeY - 1];
  };

  $: mobile = innerWidth < 640;
  $: full = !mobile;
  $: arrowPosition = mobile ? "end" : "center";
  $: activeX.join(""), activeY, updateArrows();
  $: showArrows = activeY > 0 ? ["left", "right"] : false;
  $: disableUD = activeY === 0 ? "up" : activeY === countY - 1 ? "down" : "";
  $: disableLR =
    currentX === countX[activeY - 1] - 1
      ? ["right"]
      : currentX === 0
      ? "left"
      : "";
  $: disable = [disableLR, disableUD].filter((d) => d);
</script>

<svelte:window bind:innerWidth bind:innerHeight />

<Meta {...copy} />

<Tap
  directions="{['up', 'down', 'left', 'right']}"
  showArrows="{showArrows}"
  full="{full}"
  disable="{disable}"
  enableKeyboard="{true}"
  arrowPosition="{arrowPosition}"
  on:tap="{onTap}" />

<article style="height: {innerHeight}px;">
  <Slider
    direction="vertical"
    bind:this="{sliderY}"
    bind:count="{countY}"
    bind:active="{activeY}">
    <Slide>
      <Intro hed="{copy.hed}" intro="{copy.intro}" />
    </Slide>

    {#each copy.levels as level, i}
      <Slide>
        <Slider
          direction="horizontal"
          bind:this="{sliderX[i]}"
          bind:count="{countX[i]}"
          bind:active="{activeX[i]}">
          <Slides {...level} />
        </Slider>
      </Slide>
    {/each}
  </Slider>
</article>

<style>
  article {
    width: 100%;
    height: 100vh;
    overflow: hidden;
  }
</style>
