<script>
  import { onMount } from "svelte";
  import { ARTICLE_URL } from "$lib/js/api-urls.js";

  let articles = [];

  onMount(async () => {
    await fetchArticleData();
  });

  async function fetchArticleData() {
    try {
      const response = await fetch(ARTICLE_URL);

      if (response.ok) {
        articles = await response.json();
      } else {
        console.error("Failed to fetch articles");
      }
    } catch (error) {
      console.error("Error fetching articles:", error);
    }
  }
</script>

<svelte:head>
  <title>Articles 2</title>
</svelte:head>

<div class="articles-container">
  <h1>Articles 2</h1>

  {#if articles.length > 0}
    <div class="articles-list">
      {#each articles as article}
        <div class="article-item">
          <h3>{article.title}</h3>
          <p>{article.content}</p>
          <div class="article-meta">
            <span>By {article.author}</span>
            <span>{article.date}</span>
          </div>
        </div>
      {/each}
    </div>
  {:else}
    <p>No articles found.</p>
  {/if}
</div>

<style>
  .articles-container {
    padding: 2rem;
    max-width: 800px;
    margin: 0 auto;
  }

  .articles-list {
    margin-top: 2rem;
  }

  .article-item {
    background: white;
    border-radius: 8px;
    padding: 2rem;
    margin-bottom: 1.5rem;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    border-left: 4px solid #007bff;
  }

  .article-item h3 {
    margin: 0 0 1rem 0;
    color: #333;
    font-size: 1.5rem;
  }

  .article-item p {
    margin: 0 0 1rem 0;
    color: #666;
    line-height: 1.6;
  }

  .article-meta {
    display: flex;
    justify-content: space-between;
    color: #888;
    font-size: 0.9rem;
  }

  h1 {
    text-align: center;
    color: #333;
    margin-bottom: 2rem;
  }
</style>
