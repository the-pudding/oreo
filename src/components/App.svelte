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

  let sliderY;
  let countY;

  let sliderX = [];
  let countX = [];

  const onTap = ({ detail }) => {
    if (detail === "left") sliderX.forEach((s) => s.prev());
    else if (detail === "right") sliderX.forEach((s) => s.next());
    else if (detail === "up") sliderY.prev();
    else if (detail === "down") sliderY.next();
  };

  onMount(() => {
    // sliderY.jump(2);
  });
</script>

<Meta {...copy} />

<Tap
  directions="{['up', 'down', 'left', 'right']}"
  showArrows="{false}"
  enableKeyboard="{true}"
  on:tap="{onTap}" />

<Slider direction="vertical" bind:this="{sliderY}" bind:count="{countY}">
  <Slide>
    <Intro hed="{copy.hed}" intro="{copy.intro}" />
  </Slide>

  {#each copy.levels as level, i}
    <Slide>
      <Slider
        direction="horizontal"
        bind:this="{sliderX[i]}"
        bind:count="{countX[i]}">
        <Slides {...level} />
      </Slider>
    </Slide>
  {/each}
</Slider>
