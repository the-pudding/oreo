<script>
  import { onMount } from "svelte";
  import { Swiper, SwiperSlide } from "swiper/svelte";
  import SwiperCore, { Keyboard } from "swiper";
  import Meta from "./Meta.svelte";
  import Header from "./Header.svelte";
  import Intro from "./Intro.svelte";

  let swiperInstance;
  let mounted;

  const createSwiper = (e) => {
    swiperInstance = e.detail[0];
  };

  const onSlideChange = () => {};

  onMount(() => {
    mounted = true;
    SwiperCore.use([Keyboard]);
  });
</script>

<Meta />

<Header />

{#if mounted}
  <Swiper
    direction="horizontal"
    grabCursor="{true}"
    keyboard="{true}"
    on:slideChange="{onSlideChange}"
    on:swiper="{createSwiper}">
    <SwiperSlide>
      <Intro />
    </SwiperSlide>
    <SwiperSlide>
      <Swiper direction="vertical" keyboard="{true}">
        <SwiperSlide>
          <p>
            Mini. Bite-size and snackable, the flavor without the calories. (~30
            seconds). Swipe Down.
          </p>
        </SwiperSlide>
        <SwiperSlide>
          <p>
            To some, the craziest part of 2020 was the USA Today crossword
            puzzle clue, a “cookie that some people eat with
            <mark>mustard.</mark>” The internet lost it.
          </p>
        </SwiperSlide>
        <SwiperSlide>
          <p>
            This happened because the answer &mdash;
            <strong>OREO</strong>
            &mdash; is an easy word to place in a puzzle since it contains three
            of the five most used letters.
          </p>
          <p>
            As the 7th most common four-letter answer, clues are becoming stale.
            For example, the clue "sandwich cookie" has been over 100 times
            since 1993. So
            <mark>mustard</mark>
            was used to spice things up.
          </p>
        </SwiperSlide>
        <SwiperSlide>
          <p>Swipe right for a deeper dive.</p>
        </SwiperSlide>
      </Swiper>
    </SwiperSlide>
    <SwiperSlide>
      <Swiper direction="vertical" keyboard="{true}">
        <SwiperSlide>
          <p>
            Classic. What most people would say is the right amount. (~3
            minutes). Swipe Down.
          </p>
        </SwiperSlide>
        <SwiperSlide>
          <p>
            To some, the craziest part of 2020 was the USA Today crossword
            puzzle clue, a “cookie that some people eat with
            <mark>mustard.</mark>” The internet lost it.
          </p>
        </SwiperSlide>
        <SwiperSlide>
          <p>Slide C</p>
        </SwiperSlide>
        <SwiperSlide>
          <p>Slide D</p>
        </SwiperSlide>
        <SwiperSlide>
          <p>Swipe right for an even deeper dive.</p>
        </SwiperSlide>
      </Swiper>
    </SwiperSlide>
    <SwiperSlide>
      <Swiper direction="vertical" keyboard="{true}">
        <SwiperSlide>
          <p>
            Mega Stuf. Filled with more than you need, but will probably enjoy.
            (~10+ minutes). Swipe Down.
          </p>
        </SwiperSlide>
        <SwiperSlide>
          <p>
            To some, the craziest part of 2020 was the USA Today crossword
            puzzle clue, a “cookie that some people eat with
            <mark>mustard.</mark>” The internet lost it.
          </p>
        </SwiperSlide>
        <SwiperSlide>
          <p>Slide C</p>
        </SwiperSlide>
        <SwiperSlide>
          <p>Slide D</p>
        </SwiperSlide>
        <SwiperSlide>
          <p>Slide E</p>
        </SwiperSlide>
        <SwiperSlide>
          <p>Slide F</p>
        </SwiperSlide>
        <SwiperSlide>
          <p>That is literally everything.</p>
        </SwiperSlide>
      </Swiper>
    </SwiperSlide>
  </Swiper>
{/if}

<style>
  p {
    text-align: center;
    padding-top: 10rem;
  }
</style>
