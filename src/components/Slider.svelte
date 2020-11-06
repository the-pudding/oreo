<script>
  export let name = "Version";
  const displayNames = [
    "mini",
    "thin",
    "classic",
    "double stuf",
    "mega stuf",
    "most stuf",
  ];
  let version = 0;

  $: display = displayNames[+version];
</script>

<p>{name}: {display}</p>

<input
  min="0"
  max="{displayNames.length - 1}"
  bind:value="{version}"
  type="range" />

<style>
  input {
    margin-top: 1em;
  }
</style>
