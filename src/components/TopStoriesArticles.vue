<template lang="html">
  <div class="article">
    <a :href="article.url" target="_blank">
      <article-images :imageUrl="article.urlToImage"></article-images>
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
  width: 32%;
  text-align: left;
  margin: 4px;
}

a {
  text-decoration: none;
  color: inherit;
}

.title {
  padding: 0;
  margin: 0;
  font-family: 'Open Sans';
  font-size: 20px;
  font-weight: 700;
}
</style>
