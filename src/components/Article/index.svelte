<script>
  import { onMount } from "svelte";
  import { stores } from "@sapper/app";
  import marked from "marked";

  import ArticleMeta from "./ArticleMeta.svelte";

  import hljs from "highlight.js/lib/highlight";
  import javascript from "highlight.js/lib/languages/javascript";
  import smalltalk from "highlight.js/lib/languages/smalltalk";

  onMount(() => {
    hljs.registerLanguage("javascript", javascript);
    hljs.registerLanguage("smalltalk", smalltalk);
    hljs.initHighlighting.called = false;
    hljs.initHighlighting();
  });

  const environmentConfig = require("../../config/environment");
  const config = environmentConfig.get(process.env.NODE_ENV || "production");
  const baseUrl = config.baseUrl;

  export let article;
  let markup;

  const { session } = stores();

  $: if (article) {
    markup = marked(article.body);
  }
</script>

<svelte:head>
  <title>{article.title}</title>
  <meta property="og:title" content={article.title} />
  <meta property="og:description" content={article.excerpt} />
  <meta property="og:type" content="article" />
  <meta property="og:url" content="{baseUrl}/{article.slug}/" />
  <meta property="og:image" content="{baseUrl}/profile.png" />
</svelte:head>
<div class="article-container">
  {#if article}
    <div class="banner">
      <div class="container">
        <ArticleMeta {article} user={$session.user} />
        <h2>{article.title}</h2>
        <h3>{article.subtitle}</h3>
      </div>
    </div>

    <div class="container">
      <div class="row article-content">
        <div class="col-xs-12">
          <div class="text">
            {@html markup}
          </div>

          <!-- <ul class="tag-list">
          {#each article.tags as tag}
            <li class="tag-default tag-pill tag-outline">{tag}</li>
          {/each}
        </ul> -->
        </div>
      </div>

      <hr />
      <div class="empty" />
    </div>
  {:else}
    <div class="empty">
      <div class="empty-icon">
        <i class="icon icon-3x icon-more-horiz" />
      </div>
    </div>
  {/if}
</div>

<style>
</style>
