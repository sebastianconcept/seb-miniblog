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
      <a href="/" rel="prefetch" class="home-link title-link">
        <h1>Sebastian Sastre</h1>
      </a>
    </section>
    <section class="navbar-center">
      <a href="http://sebastiansastre.co" class="btn btn-link">SITE</a>
      <!-- centered logo or brand -->
    </section>
    <section class="navbar-section">
      <Search on:search={onSearch} />
    </section>
  </header>

  <!-- <img src="/profile.png" alt="profile image" /> -->
  <!-- <div class="columns">
    <div class="col-4 ">
      <figure class="avatar badge" data-badge="8" data-initial="YZ">
        <img src="img/avatar-3.png" alt="YZ">
      </figure>
      <a href="/" rel="prefetch" class="home-link title-link">
        <h1>Sebastian Sastre</h1>
      </a>
    </div>
    <div class="col-4 ">
      <a href="http://sebastiansastre.co" rel="prefetch" class="title-link">
        SITE
      </a>
    </div>
    <div class="col-4 ">
      <Search on:search={onSearch} />
    </div>
  </div> -->
</div>

<style>
  .home-link h1 {
    margin-top: 0.6em;
    font-size: 1.4em;
    font-weight: bold;
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

  a:hover.btn-link  {
    color: #303742;
    text-decoration: none;
  }

  .header-wrapper {
    padding-top: 0.6rem;
  }
</style>
