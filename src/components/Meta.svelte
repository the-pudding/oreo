<script>
  export let hed;
  export let dek;
</script>

<svelte:head>
  <title>{hed}</title>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta http-equiv="X-UA-Compatible" content="ie=edge" />
  <meta name="description" content="{dek}" />
  <meta name="news_keywords" content="oreo, crossword, mustard" />

  <meta property="og:title" content="{hed}" />
  <meta property="og:site_name" content="The Pudding" />
  <meta property="og:url" content="https://pudding.cool/2021/01/oreo/" />
  <meta property="og:description" content="{dek}" />
  <meta property="og:type" content="article" />
  <meta property="og:locale" content="en_US" />

  <meta
    property="og:image"
    content="https://pudding.cool/2021/01/oreo/assets/img/facebook.jpg" />
  <meta property="og:image:type" content="image/jpeg" />
  <meta property="og:image:width" content="1200" />
  <meta property="og:image:height" content="600" />

  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:site" content="https://pudding.cool" />
  <meta name="twitter:creator" content="@codenberg" />
  <meta name="twitter:title" content="{hed}" />
  <meta name="twitter:description" content="{dek}" />
  <meta
    name="twitter:image:src"
    content="https://pudding.cool/2021/01/oreo/assets/img/twitter.jpg" />

  <meta name="robots" content="max-image-preview:large" />

  <link rel="canonical" href="https://pudding.cool/2021/01/oreo/" />
</svelte:head>
