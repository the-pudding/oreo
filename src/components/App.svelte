<script>
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

  let activeX = 0;
  let activeY = 0;
  let sliderY;

  const onTap = ({ detail }) => {
    if (detail === "left") activeX = Math.max(0, activeX - 1);
    // else if (detail === "right") activeX = Math.min(activeX + 1, 1);
    else if (detail === "top") sliderY.prev();
    else if (detail === "bottom") sliderY.next();
  };
</script>

<Meta {...copy} />

<Tap
  sides="{['top', 'left', 'bottom', 'right']}"
  showArrows="{true}"
  enableKeyboard="{true}"
  on:tap="{onTap}" />

<Slider direction="vertical" bind:this="{sliderY}">
  <Slide>
    <Intro hed="{copy.hed}" intro="{copy.intro}" />
  </Slide>

  {#each copy.levels as level, i}
    <Slide>
      <Slider direction="horizontal">
        <Slides {...level} />
      </Slider>
    </Slide>
  {/each}
</Slider>
