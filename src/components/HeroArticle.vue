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
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ArticleImages from './ArticleImages.vue';
export default {
  name: 'hero-article',
  props: ['articles'],
  components: {
    'article-images': ArticleImages
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
      return Math.floor(Math.random() * 100)
    }
  }
}
</script>

<style lang="css" scoped>

.overall-container {
  display: block;
  overflow: auto;
  margin-top: 25px;
  margin-bottom: 25px;
}

.article-container {
  width: 100%;
  padding: 0;
  margin: 0;
  overflow: auto;
  margin-left: 3vw;
}

.image-container {
  width: 600px;
  overflow: auto;
  border-style: solid;
  float: left;
}

.image {
  width: 600px;
  height: 500px;
}

.text-container {
  width: 600px;
  float: left;
  margin-left: 3vw;
}

.title-container {
}

.title {
  padding: 0;
  margin: 0;
  font-family: 'Coda Caption', sans-serif;
  font-size: 50px;
  font-weight: 900;
  margin-right: 25px;
  text-align: center;
}

.description-container {
  margin-top: 10px;
  display: inline-block;
  padding: 0;
  margin: 0;
}

.description {
  font-family: 'Roboto', sans-serif;
  font-weight: 900;
  font-size: 25px;
  margin-right: 25px;
  text-align: justify;
}

.content-container {
  font-size: 20px;
}

.content {
  font-family: 'Roboto', sans-serif;
  padding: 0;
  margin: 0;
  margin-right: 25px;
  text-align: justify;
}

</style>
