<template lang="html">
  <div class="article">
    <a :href="article.url" target="_blank">
      <div class="image-container">
      <article-images class="image" :imageUrl="article.urlToImage"></article-images>
      </div>
      <p class="title">{{article.title}}</p>
      <p>{{article.description}}</p>
    </a>
  </div>
</template>

<script>
import ArticleImages from './ArticleImages.vue';

export default {
  name: 'news-articles',
  props: ['article'],
  components: {
    'article-images': ArticleImages
  }
}
</script>

<style lang="css" scoped>

.article {
  border-style: solid;
  color: black;
  flex: 1, 0, auto;
  width: 240px;
  text-align: left;
  margin-right: 13px;
  margin-left: 13px;
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
  border-style: solid;
}

.image {
  width: 250px;
  height: 200px;
}

.title {
  padding: 0;
  margin: 0;
  font-family: 'Open Sans';
  font-size: 15px;
  font-weight: 900;
}
</style>
