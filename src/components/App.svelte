<script>
  import { onMount } from "svelte";
  import { csv } from "d3-fetch";
  import { Swiper, SwiperSlide } from "swiper/svelte";
  import SwiperCore, { Keyboard } from "swiper";

  import Meta from "./Meta.svelte";
  import Header from "./Header.svelte";
  import Nav from "./Nav.svelte";
  import Intro from "./Intro.svelte";
  import Slides from "./Slides.svelte";

  import { visibleIndex } from "../stores/nav.js";
  import copy from "../data/copy.json";

  SwiperCore.use([Keyboard]);

  const horizontalOptions = {
    direction: "horizontal",
    keyboard: true,
  };
  const verticalOptions = {
    direction: "vertical",
    keyboard: true,
  };

  // first is horizontal, remaining are vertical
  let swiperInstances = [];
  let mounted = true;

  const createSwiper = (e, index) => {
    swiperInstances[index] = e.detail[0];
  };

  const onHorizontalChange = ({ detail }) => {
    const [s] = detail;
    const { activeIndex } = s[0];
    if (activeIndex > 0) {
      const si = swiperInstances[activeIndex];
      $visibleIndex = si.activeIndex;
    } else $visibleIndex = 0;
  };

  const onVerticalChange = ({ detail }) => {
    const [s] = detail;
    $visibleIndex = s[0].activeIndex;
  };

  const onJump = ({ detail }) => {
    swiperInstances[0].slideTo(detail);
  };

  const cleanData = (data) => {
    return data.map((d) => ({
      ...d,
      count: +d.count,
      percent: +d.percent,
      score: +d.score,
    }));
  };

  onMount(() => {
    mounted = true;

    csv("assets/data/xd-four-letter-score-1993.csv")
      .then(cleanData)
      .then((result) => {})
      .catch((err) => {
        console.log(err);
      });
  });
</script>

<Meta {...copy} />

<Header />

<Nav levels="{copy.levels}" on:jump="{onJump}" />

{#if mounted}
  <Swiper
    {...horizontalOptions}
    on:slideChange="{onHorizontalChange}"
    on:swiper="{(e) => createSwiper(e, 0)}">
    <SwiperSlide>
      <Intro hed="{copy.hed}" intro="{copy.intro}" />
    </SwiperSlide>

    {#each copy.levels as level, i}
      <SwiperSlide>
        <Swiper
          on:slideChange="{onVerticalChange}"
          on:swiper="{(e) => createSwiper(e, i + 1)}"
          {...verticalOptions}>
          <Slides {...level} />
        </Swiper>
      </SwiperSlide>
    {/each}
  </Swiper>
{/if}
