<template lang="html">
  <div class="article">
    <a :href="article.url" target="_blank">
      <div class="image-container">
        <article-images :imageUrl="article.urlToImage"></article-images>
      </div>
      <p class="title">{{article.title}}</p>
      <article-date :publishedAt="article.publishedAt"></article-date>
    </a>
  </div>
</template>

<script>
import ArticleImages from './ArticleImages.vue';
import ArticleDate from './ArticleDate.vue';

export default {
  name: 'top-stories-articles',
  props: ['article'],
  components: {
    'article-images': ArticleImages,
    'article-date': ArticleDate,
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
  margin-right: 2%;
  margin-top: 10px;
  margin-bottom: 10px;
}

.article:hover {
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

@media screen and (max-width: 1500px) {
  .article {
    margin-right: 1%;
  }
}

@media screen and (max-width: 1400px) {
  .article {
    width: 350px;
  }

  .image-container {
    width: 360px;
  }
}

@media screen and (max-width: 1230px) {
  .article {
    width: 300px;
  }

  .image-container {
    width: 300px;
  }
}

@media screen and (max-width: 1060px) {
  .article {
    width: 250px;
  }

  .image-container {
    width: 250px;
  }
}

@media screen and (max-width: 880px) {
  .article {
    width: 95%;
  }
}

</style>
