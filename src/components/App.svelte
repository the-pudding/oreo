<script>
  import { onMount } from "svelte";
  import { csv } from "d3-fetch";
  import { Swiper, SwiperSlide } from "swiper/svelte";
  import SwiperCore, { Keyboard } from "swiper";
  import copy from "../data/copy.json";
  import Meta from "./Meta.svelte";
  import Header from "./Header.svelte";
  import Intro from "./Intro.svelte";
  import Chart from "./Chart.svelte";
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

<Meta />

<Header />

{#if mounted}
  <Swiper
    {...horizontalOptions}
    on:slideChange="{onSlideChange}"
    on:swiper="{createSwiper}">
    <SwiperSlide>
      <Intro />
    </SwiperSlide>
    {#each copy.stories as { version, slides }}
      <SwiperSlide>
        <Swiper {...verticalOptions}>
          {#each slides as { text, className, chart }}
            <SwiperSlide
              slideClass="swiper-slide {className ? `slide--${className}` : ''}">
              {#if text}
                <p>
                  {@html text}
                </p>
              {/if}
              {#if chart}
                <figure>
                  <Chart chart="{chart}" />
                </figure>
              {/if}
            </SwiperSlide>
          {/each}
        </Swiper>
      </SwiperSlide>
    {/each}
  </Swiper>
{/if}

<style>
  p {
    text-align: center;
    padding-top: 10rem;
  }
</style>
