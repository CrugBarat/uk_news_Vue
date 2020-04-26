<template lang="html">
  <div class="article">
    <a :href="article.url" target="_blank">
      <div class="image-container">
        <article-images :imageUrl="article.urlToImage"></article-images>
      </div>
      <p class="title">{{article.title}}</p>
      <p class="date">{{article.publishedAt}}</p>
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
  },
  methods: {
    articleDescription() {
      return this.article.description
    }
  }
}
</script>

<style lang="css" scoped>

.article {
  color: black;
  width: 391px;
  text-align: left;
  margin-right: 20px;
  margin-left: 20px;
  margin-top: 10px;
  margin-bottom: 10px;
}

a {
  text-decoration: none;
  color: inherit;
}

.image-container {
  width: 390px;
}

.title {
  padding: 0;
  margin: 0;
  font-family: 'Coda Caption', sans-serif;
  font-size: 20px;
  font-weight: 900;
}
</style>
