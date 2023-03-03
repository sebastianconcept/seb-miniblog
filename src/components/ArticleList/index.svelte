<script>
  import { onMount } from "svelte";
  import { stores } from "@sapper/app";
  import ArticlePreview from "./ArticlePreview.svelte";
  import InfinitePaginator from "../InfinitePaginator";
  import * as api from "../../api.js";
  import hljs from "highlight.js/lib/highlight";
  import javascript from "highlight.js/lib/languages/javascript";
  import smalltalk from "highlight.js/lib/languages/smalltalk";

  onMount(() => {
    hljs.registerLanguage("javascript", javascript);
    hljs.registerLanguage("smalltalk", smalltalk);
    hljs.initHighlighting.called = false;
    hljs.initHighlighting();
  });

  export let currentPage = 1;
  export let noItemsMessage = "No articles to display";
  let isLastPage = false;
  let isLoaded = undefined

  const { session, page } = stores();

  let query;
  let articles;
  let articlesCount;
  const pageSize = 10;

  $: {
    $session.search;
    reset();
  }

  $: {
    const endpoint = "articles";
    let params = "";
    if ($session.search) {
      params = `filter=${$session.search}&limit=${pageSize}&offset=${
        (currentPage - 1) * pageSize
      }`;
    } else {
      params = `limit=${pageSize}&offset=${(currentPage - 1) * pageSize}`;
    }

    query = `${endpoint}?${params}`;
  }

  $: query && getData();

  async function getData() {
    // TODO do we need some error handling here?
    debugger
    const answer = await api.get(query, $session.user && $session.user.token);
    isLoaded = true
    console.log('answer',answer);
    articles = articles.concat(...answer.articles);
    articlesCount = answer.articlesCount;
  }

  function reset() {
    articles = [];
    currentPage = 1;
    articlesCount = null;
    isLastPage = false;
  }

  function onPaginate(event) {
    if (articlesCount < pageSize) {
      isLastPage = true;
    }

    if (!isLastPage) {
      currentPage = currentPage + 1;
    }
  }
</script>

<div class="container">
  {#if isLoaded}
    {#if articles.length === 0}
      <div class="empty">
        <p class="empty-title h5">{noItemsMessage}</p>
      </div>
    {:else}
      <div class="articles">
        {#each articles as article (article.slug)}
          <ArticlePreview {article} />
        {/each}
        <InfinitePaginator on:paginate={onPaginate} />
      </div>
    {/if}
  {:else}
    <div class="loading loading-lg" />
  {/if}
</div>

<style>
.loading {
  margin-top: 3rem;
}
</style>
