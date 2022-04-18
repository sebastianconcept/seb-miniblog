<script>
  import { onMount } from "svelte";

  import { goto, stores } from "@sapper/app";
  const { session, page } = stores();

  $session.search = $page.query.search || "";

  export let searchTarget = $session.search;

  function onSubmit(event) {
    if (searchTarget !== $session.search) {
      $session.search = searchTarget;
      goto(`/?search=${$session.search}`);
    }
  }

  function onReset(event) {
    searchTarget = "";
    onSubmit(event);
  }
</script>

<div class="search">
  <form class="form-group" on:submit|preventDefault={onSubmit}>
    <div class="input-group">
      <input
        class="form-input "
        type="text"
        placeholder="Search by title or content"
        bind:value={searchTarget}
      />
      <div class="btn-group form-inline">
        <button class="btn input-group-btn" type="submit">
          <i class="icon icon-search" />
        </button>
        {#if searchTarget}
          <button class="btn" on:click={onReset}>
            <i class="icon icon-refresh" />
          </button>
        {/if}
      </div>
    </div>
  </form>
</div>

<style>
  input {
    margin-right: 0.25em;
  }
  @media screen and (max-width: 600px) {
    .search {
      width: 12em;
    }
    input {
      font-size: 0.7em;
    }
  }

  @media screen and (min-width: 601px) {
    .search {
      width: 18em;
    }
  }

  .btn {
    color: #ffffff;
  }

  .btn:focus,
  .btn:hover {
    color: #303742;
    background: #f1f1fc;
    border-color: #2a5572;
    text-decoration: none;
  }

  button {
    background-color: #303742;
  }
</style>
