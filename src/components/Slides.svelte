<script>
  import { SwiperSlide } from "swiper/svelte";
  import Oreo from "./Oreo.svelte";
  import Chart from "./Chart.svelte";
  import Special from "./Special.svelte";
  import Image from "./Image.svelte";
  import Icon from "./helpers/Icon.svelte";

  export let version;
  export let level;
  export let duration;
  export let text;
  export let slides;
</script>

<SwiperSlide>
  <div class="slide-content intro">
    <p class="level">Level {level}</p>
    <p class="version"><strong>{version}</strong></p>
    <Oreo version="{version}" />
    <p class="duration">~ {duration}</p>
    <p class="text">{text}</p>
    <button>
      <Icon name="triangle" direction="s" />
    </button>
  </div>
</SwiperSlide>

{#each slides as { text, className, chart, special, image }}
  <SwiperSlide>
    <div class="slide-content {className || ''}">
      {#if typeof text === 'string'}
        <div class="graf">
          <p>
            {@html text}
          </p>
        </div>
      {:else if typeof text === 'object'}
        <div class="graf">
          {#each text as { value }}
            <p>
              {@html value}
            </p>
          {/each}
        </div>
      {/if}

      {#if chart}
        <div class="chart">
          <Chart name="{chart}" />
        </div>
      {/if}

      {#if special}
        <div class="special">
          <Special name="{special}" />
        </div>
      {/if}

      {#if image}
        <Image name="{image}" />
      {/if}
    </div>
  </SwiperSlide>
{/each}

<style>
  .slide-content {
    padding-left: 1rem;
    padding-right: 1rem;
    display: flex;
    flex-direction: column;
    height: 100%;
    max-width: 40em;
    margin: 0 auto;
    overflow: hidden;
  }

  .intro {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100%;
    font-size: 3vh;
  }

  .intro p {
    margin: 0.5em 0;
  }

  .level {
    opacity: 0.5;
  }

  .version {
    text-transform: capitalize;
    font-size: 2em;
  }

  .duration {
  }

  .oreo {
    width: 16em;
    height: 16em;
  }

  .text {
    font-size: 1.25em;
  }

  button {
    background: none;
    color: var(--fg);
    font-size: 2em;
  }

  .reverse {
    flex-direction: column-reverse;
  }

  @media only screen and (min-width: 640px) {
    .slide-content {
      justify-content: center;
    }
  }
</style>