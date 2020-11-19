<script>
  import { onMount } from "svelte";
  import { csv } from "d3-fetch";
  import { Swiper, SwiperSlide } from "swiper/svelte";
  import SwiperCore, { Keyboard } from "swiper";

  import Meta from "./Meta.svelte";
  import Header from "./Header.svelte";
  import Intro from "./Intro.svelte";
  import Slides from "./Slides.svelte";

  import copy from "../data/copy.json";
  import popularData from "../data/xd-four-letter-popular-1993.csv";

  SwiperCore.use([Keyboard]);

  const horizontalOptions = {
    direction: "horizontal",
    keyboard: true,
  };
  const verticalOptions = {
    direction: "vertical",
    keyboard: true,
  };

  let swiperInstance;
  let mounted = true;

  const createSwiper = (e) => {
    swiperInstance = e.detail[0];
  };

  const onSlideChange = () => {};

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

{#if mounted}
  <Swiper
    {...horizontalOptions}
    on:slideChange="{onSlideChange}"
    on:swiper="{createSwiper}">
    <SwiperSlide>
      <Intro hed="{copy.hed}" />
    </SwiperSlide>

    {#each copy.levels as level}
      <SwiperSlide>
        <Swiper {...verticalOptions}>
          <Slides {...level} />
        </Swiper>
      </SwiperSlide>
    {/each}
  </Swiper>
{/if}
