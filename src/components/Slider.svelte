<script>
  export let name = "Version";
  const displayNames = ["Oreo mini", "Thin Oreo", "Classic Oreo"];
  let version = 0;

  $: display = displayNames[+version];
</script>

<p>{name}: {display}</p>

<input min="0" max="2" bind:value="{version}" type="range" />

<style>
  input {
    margin-top: 1em;
  }
</style>
