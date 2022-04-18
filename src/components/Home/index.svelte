<script>
  import Header from "../Header";
  import ArticleList from "../ArticleList";

  const showPublishingState = false;
  const selection = "published";
  const noItemsMessage = "No articles matching that";
</script>

<div class="home-page">
  <div class="container">
    <Header />
    <div class=" main-column">
      <ArticleList {showPublishingState} {selection} {noItemsMessage} />
    </div>
  </div>
</div>

<style>
  .header {
    background-color: #303742;
    padding-bottom: 1rem;
  }
  .main-column {
    margin-right: 0;
  }
</style>
