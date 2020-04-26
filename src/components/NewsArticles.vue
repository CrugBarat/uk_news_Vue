<template lang="html">
  <div class="article">
    <a :href="article.url" target="_blank">
      <div class="image-container">
      <article-images class="image" :imageUrl="article.urlToImage"></article-images>
      </div>
      <p class="title">{{article.title}}</p>
      <p class="description">{{article.description}}</p>
      <article-date :publishedAt="article.publishedAt"></article-date>
    </a>
  </div>
</template>

<script>
import ArticleImages from './ArticleImages.vue';
import ArticleDate from './ArticleDate.vue';

export default {
  name: 'news-articles',
  props: ['article'],
  components: {
    'article-images': ArticleImages,
    'article-date': ArticleDate,
  }
}
</script>

<style lang="css" scoped>

.article {
  color: black;
  flex: 1, 0, auto;
  width: 240px;
  text-align: left;
  margin-right: 17px;
  margin-left: 17px;
  margin-top: 10px;
  margin-bottom: 10px;
  overflow: auto;
}

a {
  text-decoration: none;
  color: inherit;
}

.image-container {
  width: 250px;
  overflow: auto;
}

.image {
  width: 250px;
  height: 200px;
}

.title {
  padding: 0;
  margin: 0;
  font-family: 'Coda Caption', sans-serif;
  font-size: 15px;
  font-weight: 900;
}

.description {
  font-family: 'Roboto', sans-serif;
}
</style>
