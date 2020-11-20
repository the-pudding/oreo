<script>
  import { onMount } from "svelte";
  import { shuffle } from "d3-array";
  const v = Date.now();
  const url = `https://pudding.cool/assets/data/stories.json?v=${v}`;

  let localURL;

  onMount(() => {
    localURL = window.location.href;
  });

  const fetchData = (async () => {
    const response = await fetch(url);
    const data = await response.json();
    const stories = shuffle(data.filter((d) => d.url !== localURL)).slice(0, 5);
    return stories;
  })();
</script>

{#await fetchData then data}
  {#each data as { hed, url, image }}
    <div class="story">
      <p><a href="{url}">{hed}</a></p>
    </div>
  {/each}
{/await}

<style>
  p {
    display: flex;
    align-items: center;
    margin-bottom: 1.5em;
  }

  a {
    /* margin-left: 1em; */
  }
</style>
