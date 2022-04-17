<script>
  import marked from "marked";
  import ArticleMeta from "../Article/ArticleMeta";
  import { onMount } from "svelte";
  import hljs from "highlight.js/lib/highlight";
  import javascript from "highlight.js/lib/languages/javascript";
  import smalltalk from "highlight.js/lib/languages/smalltalk";

  export let article;
  let markup;

  $: if (article) {
    markup = marked(getExcerpt(article));
  }

  export function getExcerpt(article) {
    if (article.excerpt) {
      return article.excerpt;
    } else {
      return article.body.split("\n")[0];
    }
  }


  onMount(() => {
    hljs.registerLanguage("javascript", javascript);
    hljs.registerLanguage("smalltalk", smalltalk);
    hljs.initHighlighting.called = false;
    hljs.initHighlighting();
  });
</script>

<div class="article-preview">
  <ArticleMeta {article} />
  <a
    href="/article/{article.slug}"
    rel="prefetch"
    class="preview-link title-link"
  >
    <h2>{article.title}</h2>
  </a>
  <h3>{article.subtitle}</h3>
  <div class="text excerpt-text">
    {@html markup}
  </div>
</div>

<style>
  .title-link {
    color: #303742;
  }
</style>
