<template lang="html">
  <div class="overall-container">
    <div v-for="article in heroArticles(randomIndex())">
      <div class="article-container">
        <div class="image-container">
          <a :href="article.url" target="_blank">
            <article-images class="image" :imageUrl="article.urlToImage"></article-images>
          </a>
        </div>
        <div class="text-container">
          <div class="title-container">
            <p class="title">{{article.title}}</p>
          </div>
          <div class="description-container">
            <p class="description">{{article.description}}</p>
          </div>
          <div class="content-container">
            <p class="content">{{article.content}}</p>
          </div>
          <article-date class="date" :publishedAt="article.publishedAt"></article-date>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ArticleImages from './ArticleImages.vue';
import ArticleDate from './ArticleDate.vue';

export default {
  name: 'hero-article',
  props: ['articles'],
  components: {
    'article-images': ArticleImages,
    'article-date': ArticleDate,
  },
  methods: {
    heroArticles(index) {
      let articles = this.articles;
      let i, j, chunkedArray = [], chunk = 1;
      for (i=0, j=0; i < articles.length; i += chunk, j++) {
        chunkedArray[j] = articles.slice(i,i+chunk);
      }
      return chunkedArray[index];
    },
    randomIndex() {
      return Math.floor(Math.random() * 98)
    }
  }
}
</script>

<style lang="css" scoped>

.overall-container {
  display: block;
  text-align: center;
  margin-top: 25px;
  margin-bottom: 25px;
}

.article-container {
  width: 80%;
  display: inline-block;
  padding: 0;
  margin: 0;
}

.image-container {
  width: 600px;
  height: 100%;
  float: left;
  margin-right: 5vw;
}

.image {
  width: 600px;
  height: 500px;
}

.text-container {
  width: 45%;
  float: left;
}

.title-container {
}

.title {
  padding: 0;
  margin: 0;
  font-family: 'Coda Caption', sans-serif;
  font-size: 50px;
  font-weight: 900;
  text-align: center;
}

.description-container {
  margin-top: 10px;
  padding: 0;
  margin: 0;
}

.description {
  font-family: 'Roboto', sans-serif;
  font-weight: 900;
  font-size: 25px;
  text-align: justify;
}

.content-container {
  font-size: 20px;
}

.content {
  font-family: 'Roboto', sans-serif;
  padding: 0;
  margin: 0;
  text-align: justify;
}

.date {
  text-align: left;
}

</style>
