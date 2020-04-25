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
  border-style: solid;
  color: black;
  flex: 1, 0, auto;
  width: 391px;
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
  width: 390x;
  overflow: auto;
  border-style: solid;
}

.title {
  padding: 0;
  margin: 0;
  font-family: 'Open Sans';
  font-size: 20px;
  font-weight: 700;
}
</style>
