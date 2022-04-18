<script>
  export let article;

  let date = article.publishedAt || article.createdAt;

  function words() {
    return article.body.split(" ").length;
  }
</script>

<div class="article-meta">
  <div class="info float-left">
    <span class="date-and-read-time"
      >{new Date(date).toLocaleDateString("en-us", {
        day: "numeric",
        year: "numeric",
        month: "long",
      })} ・ {Math.round(words()/200)} min read</span
    >
  </div>
</div>

<style>
  .date-and-read-time {
    color: #aaa;
    font-size: 0.8em;
  }
  .article-meta {
    display: inline-block;
    width: 100%;
  }
</style>
