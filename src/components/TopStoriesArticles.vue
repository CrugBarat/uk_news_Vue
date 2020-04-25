<template lang="html">
  <div class="article">
    <a :href="article.url" target="_blank">
      <div class="image-container">
        <article-images :imageUrl="article.urlToImage"></article-images>
      </div>
      <p class="title">{{article.title}}</p>
    </a>
  </div>
</template>

<script>
import ArticleImages from './ArticleImages.vue';

export default {
  name: 'top-stories-articles',
  props: ['article'],
  components: {
    'article-images': ArticleImages
  }
}
</script>

<style lang="css" scoped>

.article {
  color: black;
  flex: 1, 0, auto;
  width: 391px;
  text-align: left;
  margin-right: 20px;
  margin-left: 20px;
  margin-top: 10px;
  margin-bottom: 10px;
  overflow: auto;
}

a {
  text-decoration: none;
  color: inherit;
}

.image-container {
  width: 390px;
  overflow: auto;
}

.title {
  padding: 0;
  margin: 0;
  font-family: 'Coda Caption', sans-serif;
  font-size: 20px;
  font-weight: 900;
}
</style>
