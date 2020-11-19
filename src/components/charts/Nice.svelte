<script>
  export let data = [{ x: 50, y: 50 }];
</script>

<svg>
  <g>
    {#each data as d}
      <circle cx="{d.x}" cy="{d.y}" r="3"></circle>
    {/each}
  </g>
</svg>

<style>
</style>
