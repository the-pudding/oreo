<script>
  export let name;

  const data = {
    email: {
      src: "email.jpg",
      alt: "Screenshot of an email from a tweet",
      caption:
        "Letter to the editor of the USA Today crossword screenshot from <a href='https://twitter.com/smileyb97/status/1228105944061685760'>a tweet.</a>",
    },
    mukbang: {
      src: "mukbang.jpg",
      alt: "Screenshot of two people eating oreos with mustard",
      caption:
        "Shay Mitchell tries an Oreo with mustard on <a href='https://www.youtube.com/watch?v=FA1FCW_DmEI?t=83'>YouTube.</a>",
    },
    aoc: {
      src: "aoc.jpg",
      alt: "Screenshot of Ken Jennings tweet about AOC and LBJ",
      caption:
        "Ken Jennings <a href='https://twitter.com/KenJennings/status/1070120490864336896'>tweeting</a> crossword constructing tips.",
    },
    chef: {
      src: "chef.png",
      alt: "Chef kiss",
      caption: "",
    },
  };
</script>

<figure>
  <img
    loading="lazy"
    src="assets/img/{data[name].src}"
    alt="{data[name].alt}" />
  <figcaption>
    {@html data[name].caption}
  </figcaption>
</figure>

<style>
  figure {
    margin: 0 auto;
    max-width: 27em;
    padding: 1em;
  }
  img {
    border-radius: 4px;
    box-shadow: 0 0 8px 0px var(--fg);
  }
  figcaption {
    margin-top: 1em;
    font-style: italic;
    font-size: 0.75em;
  }
</style>
