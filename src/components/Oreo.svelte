<script>
  export let version = "classic";
  const versions = {
    mini: {
      w: 4,
      t: 3,
    },
    classic: {
      w: 8,
      t: 0,
    },
    "mega stuf": {
      w: 8,
      t: 10,
    },
  };
  let cl = version.toLowerCase().replace(" ", "");
  let cw = 1;
  let v = versions[version];
  $: h = Math.floor(0.9 * cw);
  $: w = v.w;
  $: tm = 5 + v.t;
  $: ts = 7 + v.t;
  $: tb = 12 + v.t;
</script>

<div class="cookie">
  <div class="outer {cl}" style="height: {h}px;">
    <div style="width: {w}em;" class="oreo" bind:offsetWidth="{cw}">
      <div class="top"></div>
      <div style="top: {tm}%" class="middle"></div>
      <div style="top: {ts}%" class="shadow"></div>
      <div style="top: {tb}%" class="bottom"></div>
    </div>
  </div>
</div>

<style>
  .cookie {
    height: 8em;
    width: 100%;
    display: flex;
    align-items: center;
  }

  .outer {
    position: relative;
    width: 100%;
    top: 0;
    left: 0;
    margin: 0 auto;
  }

  .oreo {
    position: absolute;
    margin: auto;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
  }
  .top {
    width: 100%;
    height: 60%;
    border-radius: 50%;
    background-color: var(--brown);
    position: absolute;
    z-index: 5;
  }
  .middle {
    width: 100%;
    height: 60%;
    border-radius: 50%;
    background-color: var(--white);
    background-image: none;
    position: absolute;
    z-index: 3;
    top: 5%;
  }
  .megastuf .middle {
    border-top-left-radius: 35%;
    border-top-right-radius: 35%;
  }
  .shadow {
    width: 100%;
    height: 60%;
    border-radius: 50%;
    background-color: var(--off-white);
    background-image: none;
    position: absolute;
    z-index: 2;
    top: 7%;
  }
  .bottom {
    width: 100%;
    height: 60%;
    border-radius: 50%;
    background-color: var(--brown);
    background-image: none;
    position: absolute;
    z-index: 1;
    top: 12%;
  }
</style>
