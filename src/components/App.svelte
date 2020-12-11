<script>
  import { onMount } from "svelte";
  import { Swiper, SwiperSlide } from "swiper/svelte";
  import SwiperCore, { Keyboard } from "swiper";

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

  let active = 0;

  SwiperCore.use([Keyboard]);

  const options = {
    keyboard: true,
    allowTouchMove: false,
    speed: 500,
    // shortSwipes: false,
    // longSwipesRatio: 0.1,
    // simulateTouch: false,
  };

  const levelOptions = {
    ...options,
    direction: "vertical",
  };
  const storyOptions = {
    ...options,
    direction: "horizontal",
  };

  // first is vertical, remaining are horizontal
  let swiperInstances = [];
  let mounted = false;

  const createSwiper = (e, index) => {
    swiperInstances[index] = e.detail[0];
  };

  const onLevelChange = ({ detail }) => {
    const [s] = detail;
    const { activeIndex } = s[0];
    if (activeIndex > 0) {
      const si = swiperInstances[activeIndex];
      $visibleIndex = si.activeIndex;
    } else $visibleIndex = 0;
  };

  const onStoryChange = ({ detail }) => {
    const [s] = detail;
    $visibleIndex = s[0].activeIndex;
  };

  const onJump = ({ detail }) => {
    swiperInstances[0].slideTo(detail);
  };

  const onTap = ({ detail }) => {
    const inc = detail === "right" ? 1 : -1;
    active += inc;
  };

  onMount(() => {
    mounted = false;
    // // TODO remove
    // setTimeout(() => {
    //   swiperInstances[0].slideTo(3);
    //   swiperInstances[3].slideTo(16);
    // }, 100);
  });
</script>

<Meta {...copy} />

<!-- <Nav levels="{copy.levels}" on:jump="{onJump}" /> -->
<Tap debug="{false}" showArrows="{true}" on:tap="{onTap}" />
<Slider direction="vertical" active="{active}">
  <Slide>
    <p>Whatup big fella?</p>
  </Slide>

  <Slide>
    <img
      src="https://www.mercurynews.com/wp-content/uploads/2019/10/BNG-L-WARRIORS-1011-18.jpg?w=1368" />
  </Slide>
</Slider>

{#if mounted}
  <Swiper
    {...levelOptions}
    on:slideChange="{onLevelChange}"
    on:swiper="{(e) => createSwiper(e, 0)}">
    <SwiperSlide>
      <Intro hed="{copy.hed}" intro="{copy.intro}" />
    </SwiperSlide>

    {#each copy.levels as level, i}
      <SwiperSlide>
        <Swiper
          on:slideChange="{onStoryChange}"
          on:swiper="{(e) => createSwiper(e, i + 1)}"
          {...storyOptions}>
          <Slides {...level} />
        </Swiper>
      </SwiperSlide>
    {/each}
  </Swiper>
{/if}
