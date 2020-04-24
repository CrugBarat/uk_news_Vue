<template lang="html">
  <div class="article">
    <a :href="article.url" target="_blank">
      <article-images class="article-image" :imageUrl="article.urlToImage"></article-images>
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
  width: 19%;
  text-align: left;
  margin: 4px;
}

a {
  text-decoration: none;
  color: inherit;
}

.article-image {
  width: 270px;
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
