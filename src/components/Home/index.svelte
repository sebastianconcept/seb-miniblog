<script>
  import { onMount } from "svelte";
  import { stores } from "@sapper/app";
  const { session, page } = stores();

  import Header from "../Header";
  import ArticleList from "../ArticleList";
  import SidebarMenu from "../SidebarMenu";

  let queryParams = {};
  const showPublishingState = false;
  const selection = "published";
</script>

<div class="home-page">
  <div class="container">
    <Header />
    <!-- <div class="columns header">
    </div> -->
    <div class="columns main-columns">
      <div class="col-8 col-sm-12 float-right ">
        <ArticleList {showPublishingState} {selection} />
      </div>
      <div class="col-4 col-sm-12 float-left sidebar-container">
        <SidebarMenu />
      </div>
    </div>
  </div>
</div>

<style>
  .header {
    background-color: #303742;
    padding-bottom: 1rem;
  }

  .main-columns {
    margin-right: 0;
  }
</style>
