<script>
</script>

<svelte:head>
  <!-- Google tag (gtag.js) -->
  <script
    async
    src="https://www.googletagmanager.com/gtag/js?id=G-5X80G74H20"
  ></script>
  <script>
    window.dataLayer = window.dataLayer || [];
    function gtag() {
      dataLayer.push(arguments);
    }
    gtag("js", new Date());

    gtag("config", "G-5X80G74H20");
  </script>
</svelte:head>

<main>
  <slot />
</main>

<style>
  main {
    position: relative;
    max-width: 66em;
    background-color: white;
    padding: 0 2em;
    margin: 0 auto;
    box-sizing: border-box;
  }
</style>
