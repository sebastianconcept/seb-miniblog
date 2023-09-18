<script>
  export let article;
  let updatedAt = new Date(article.updatedAt).toLocaleDateString("en-us", {
    day: "numeric",
    year: "numeric",
    month: "long",
  });

  let publishedAt = new Date(article.publishedAt).toLocaleDateString("en-us", {
    day: "numeric",
    year: "numeric",
    month: "long",
  });

  function words() {
    return article.body.split(" ").length;
  }
</script>

<div class="article-meta">
  <div class="info float-left">
    {#if article.publishedAt}
    <span class="date-and-read-time"
      >{publishedAt} ・ {Math.round(words() / 200)} min read</span
    >
    {:else}
    <span class="date-and-read-time"
    >Updated on {updatedAt} DRAFT・ {Math.round(words() / 200)} min read</span
  >
    {/if}
  </div>
</div>

<style>
  .date-and-read-time {
    color: #6B6B6B;
    font-size: 0.8em;
  }
  .article-meta {
    display: inline-block;
    width: 100%;
    margin-top: 1em;
  }
</style>
