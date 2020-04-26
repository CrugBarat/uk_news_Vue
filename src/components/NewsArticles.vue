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
  width: 17%;
  text-align: left;
  margin-right: 1%;
  margin-left: 1%;
  margin-top: 10px;
  margin-bottom: 10px;
}

a {
  text-decoration: none;
  color: inherit;
}

.image-container {
  width: 100%;
  overflow: auto;
}

.image {
  width: 100%;
  height: auto;
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

@media screen and (max-width: 1550px) {
  .article {
    width: 20%;
  }
}

@media screen and (max-width: 1250px) {
  .article {
    width: 30%;
  }
}

@media screen and (max-width: 630px) {
  .article {
    width: 45%;
  }
}

@media screen and (max-width: 630px) {
  .article {
    width: 95%;
  }
}
</style>
