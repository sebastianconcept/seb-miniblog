<script>
  import Search from "../Search.svelte";
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  function onSearch(event) {
    dispatch("search", event.detail);
  }
</script>

<div class="header-wrapper">
  <header class="navbar">
    <section class="navbar-section">
      <figure class="avatar subject-avatar">
        <img src="/avatar.png" alt="avatar">
      </figure>
      <a href="/" rel="prefetch" class="home-link title-link">
        <h1>Sebastian Sastre</h1>
      </a>
    </section>
    <section class="navbar-center hide-sm social-links">
      <a href="http://sebastiansastre.co" class="btn btn-link">WEBSITE</a>
      <a href="http://github.com/sebastianconcept" class="btn btn-link github">
        <img src="/github.png" alt="github" />
      </a>
    </section>
    <section class="navbar-section right-section">
      <Search on:search={onSearch} />
    </section>
  </header>
</div>

<style>
  @media screen and (max-width: 600px) {
    .home-link h1 {
      position: relative;
      left: 7px;
      margin-top: 0.6em;
      font-size: 0.8em;
    }
    .subject-avatar {
      width: 24px;
      height: 24px;
    }
  }

  @media screen and (min-width: 601px) {
    .home-link h1 {
      position: relative;
      left: 7px;
      margin-top: 0.7em;
      font-size: 1.4em;
    }
    .subject-avatar {
      width: 48px;
      height: 48px;
    }
  }
  .home-link h1 {
    margin-top: 0.6em;
    font-weight: bold;
  }

  .github img {
    width: 20px;
  }

  a.home-link {
    color: #303742;
  }
  a.home-link:hover {
    text-decoration: none;
  }

  a.btn-link {
    color: #303742;
  }

  a:hover.btn-link {
    color: #303742;
    text-decoration: none;
  }

  .social-links {
    margin-top: 5px;
  }
  .header-wrapper {
    padding-top: 0.6rem;
  }
</style>
