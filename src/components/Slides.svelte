<script>
  import { SwiperSlide } from "swiper/svelte";
  import Chart from "./Chart.svelte";

  export let version;
  export let level;
  export let duration;
  export let text;
  export let slides;
</script>

<SwiperSlide>
  <div class="slide-content">
    <p>Level {level}</p>
    <p>~ {duration}</p>
    <p>{text}</p>
  </div>
</SwiperSlide>

{#each slides as { text, className, chart }}
  <SwiperSlide>
    <div class="slide-content {className || ''}">
      {#if typeof text === 'string'}
        <p>
          {@html text}
        </p>
      {:else if typeof text === 'object'}
        {#each text as { value }}
          <p>
            {@html value}
          </p>
        {/each}
      {/if}
      {#if chart}
        <figure>
          <Chart name="{chart}" />
        </figure>
      {/if}
    </div>
  </SwiperSlide>
{/each}

<style>
  .slide-content {
    padding: 1rem;
  }
  .slide-content.version {
    font-size: 2em;
  }
</style>
