<script>
  import { onMount } from "svelte";
  import { stores } from "@sapper/app";
  import marked from "marked";
  import Header from "../Header";
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

<div class="article-container">
  <div class="article-header">
    <Header />
  </div>

  {#if article}
    <div class="page">
      <div class="page-header">
        <div class="container">
          <h2>{article.title}</h2>
          {#if article.subtitle}
            <h3>{article.subtitle}</h3>
          {/if}
          <ArticleMeta {article} user={$session.user} />
        </div>
      </div>

      <div class="page-body">
        <div class="row article-content">
          <div class="col-xs-12">
            <div class="text">
              {@html markup}
            </div>
          </div>
        </div>
      </div>
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
  .article-header {
    margin-bottom: 30px;
  }

  h2 {
    margin-bottom: -0.27em;
  }

  h3 {
    margin-top: 0.92em;
    font-style: normal;
    letter-spacing: 0;
    color: #6b6b6b;
    font-weight: normal;
  }
  /* h3,
  h2 {
    color: #303742;
  }
  
  h2 {
    margin-bottom: 0.2em;
  }
  h3 {
    font-size: 1.3em;
  } */
</style>
