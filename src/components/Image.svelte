<script>
  export let name;

  const data = {
    email: {
      src: "email.jpg",
      alt: "Screenshot of an email from a tweet",
      caption:
        "Letter to the editor of the USA Today crossword screenshot from <a href=https://twitter.com/smileyb97/status/1228105944061685760>a tweet.</a>",
    },
    mukbang: {
      src: "mukbang.jpg",
      alt: "Screenshot of two people eating oreos with mustard",
      caption:
        "Shay Mitchell tries an Oreo with mustard on <a href=https://www.youtube.com/watch?v=FA1FCW_DmEI?t=83>YouTube.</a>",
    },
  };
</script>

<figure>
  <img src="assets/img/{data[name].src}" alt="{data[name].alt}" />
  <figcaption>
    {@html data[name].caption}
  </figcaption>
</figure>

<style>
  img {
    border-radius: 4px;
    box-shadow: 0 0 4px 0px var(--fg);
  }
  figcaption {
    margin-top: 0.5em;
    font-style: italic;
  }
</style>
