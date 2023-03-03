<script context="module">
  import * as api from "../../api.js";

  export async function preload({ params }) {
    const { slug } = params;

    const article = await api.get(`articles/${slug}`, null);
    return { article, slug };
  }
  const environmentConfig = require("../../config/environment");
  const config = environmentConfig.get(process.env.NODE_ENV || "production");
  const baseUrl = config.baseUrl;
  const imageUrl = `${baseUrl}/profile.png`;
</script>

<script>
  import { goto } from "@sapper/app";

  import Article from "../../components/Article";
  // import SidebarMenu from "../../components/SidebarMenu";

  export let article;
  const fullURL = `${baseUrl}/${article.slug}/`;
  const imageUrl = extractImageUrls(article.body) || `${baseUrl}/profile.png`;

  function onSearch(event) {
    goto(`/?search=${event.detail.target}`);
  }

  function extractImageUrls(str) {
    const regex = /(https?:\/\/[^\s]+\.(?:jpe?g|png|gif|bmp|webp))/gi;
    const matches = str.match(regex);
    return matches ? matches[0] : null;
  }
</script>

<svelte:head>
  <title>{article.title}</title>
  <meta property="og:title" content={article.title} />
  <meta property="og:description" content={article.excerpt} />
  <meta property="og:type" content="article" />
  <meta property="og:url" content={fullURL} />
  <meta property="og:image" content={imageUrl} />

  <meta property="og:site_name" content="Sebastian Sastre" />

  <meta property="twitter:title" content={article.title} />
  <meta property="twitter:description" content={article.excerpt} />
  <meta property="twitter:image" content={imageUrl} />
  <meta property="twitter:card" content={imageUrl} />
  <meta name="author" content="Sebastian Sastre" />
  <meta name="description" content={article.excerpt} />
  <meta property="article:published_time" content={article.publishedAt} />
</svelte:head>

<div class="article-page">
  <div class="container">
    <Article {article} />
  </div>
</div>
