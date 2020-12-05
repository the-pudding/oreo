<svg width="{width}" height="{height}">
  <g transform="translate({pad}, {pad})">
    {#each highlightData as { answer, prob, count }}
      <g
        class:highlight="{answer === 'OREO'}"
        class:visible="{answer === 'OREO'}"
        transform="translate({scaleX(prob)}, {scaleY(count)})">
        <text
          class="bg"
          y="-8"
          alignment-baseline="baseline"
          text-anchor="middle">
          {answer}
        </text>
        <text
          class="fg"
          y="-8"
          alignment-baseline="baseline"
          text-anchor="middle">
          {answer}
        </text>
        <circle cx="0" cy="0" r="{r}"></circle>
      </g>
    {/each}
  </g>
</svg>

<style>
  circle {
    fill: var(--primary);
  }

  text {
    fill: var(--primary);
    font-weight: var(--bold);
  }

  text.bg {
    stroke: var(--bg);
    stroke-width: 4px;
    fill: none;
  }

  svg {
    position: absolute;
    top: 0;
    left: 0;
  }

  canvas {
    position: absolute;
    top: 0;
    left: 0;
  }
</style>
