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
  <title>Articles 1</title>
</svelte:head>

<div class="articles-container">
  <h1>Articles 1</h1>

  {#if articles.length > 0}
    <div class="articles-grid">
      {#each articles as article}
        <div class="article-card">
          <h3>{article.title}</h3>
          <p>{article.content}</p>
          <small>By {article.author} on {article.date}</small>
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
    max-width: 1200px;
    margin: 0 auto;
  }

  .articles-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 1.5rem;
    margin-top: 2rem;
  }

  .article-card {
    background: white;
    border-radius: 8px;
    padding: 1.5rem;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    border: 1px solid #e1e5e9;
  }

  .article-card h3 {
    margin: 0 0 1rem 0;
    color: #333;
  }

  .article-card p {
    margin: 0 0 1rem 0;
    color: #666;
    line-height: 1.5;
  }

  .article-card small {
    color: #888;
  }

  h1 {
    text-align: center;
    color: #333;
    margin-bottom: 2rem;
  }
</style>
