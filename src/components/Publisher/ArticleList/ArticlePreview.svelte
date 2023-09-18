<script>
  import marked from "marked";
  import ArticleMeta from "../../Article/ArticleMeta";

  export let article;
  let markup = "";

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
</script>

<div class="page-header">
  <div class="container">
    <a
      href="/article/{article.slug}"
      rel="prefetch"
      class="preview-link title-link"
    >
      <h2>{article.title}</h2>
    </a>
    {#if article.subtitle}
      <h3>{article.subtitle}</h3>
    {/if}
    <ArticleMeta {article} />
  </div>
</div>
<div class="text excerpt-text">
  {@html markup}
</div>

<style>
  .excerpt-text {
    margin: 1em 0;
  }

  a {
    display: block;
  }
  .title-link,
  h2 {
    margin-bottom: -0.27em;
    text-decoration: none;
  }

  h3 {
    margin-top: 0.92em;
    font-style: normal;
    letter-spacing: 0;
    color: #6b6b6b;
    font-weight: normal;
  }

</style>
