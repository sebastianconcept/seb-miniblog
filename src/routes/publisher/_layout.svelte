<script context="module">
  export function preload(page, session) {
    if (!hasSinedIn(session)) {
      this.redirect(302, "/sign-in");
    }

    function hasSinedIn(session) {
      return !!session.user;
    }
  }
</script>

<script>
  import Nav from "../../components/Nav.svelte";
  export let segment;
</script>

<!-- {#if preloading}
  <div class="loading loading-lg" />
{/if} -->

<main>
  <slot />
</main>

<style>
  main {
    position: relative;
    max-width: 66em;
    background-color: white;
    margin: 0 auto;
    box-sizing: border-box;
  }
</style>
