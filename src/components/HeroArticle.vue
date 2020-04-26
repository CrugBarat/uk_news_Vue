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
            <p class="title">{{article.title}}</p>
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
  width: 90%;
  display: inline-block;
  margin-left: 5%;
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

.content {
  font-family: 'Roboto', sans-serif;
  font-size: 20px;
  text-align: justify;
  padding: 0;
  margin: 0;
}

.date {
  text-align: left;
}

@media screen and (max-width: 1600px) {
  .article-container {
    margin-left: 0%;
    width: 95%;
  }

  .image-container {
    margin-right: 2.5vw;
  }
}

@media screen and (max-width: 1375px) {
  .article-container {
    width: 100%;
  }
  .image-container {
    width: 500px;
    height: 100%;
    margin-right: 1.25vw;
  }

  .image {
    width: 500px;
    height: 400px;
  }

  .title {
    font-size: 40px;
  }

  .description {
    font-size: 20px;
  }

  .content {
    font-size: 15px;
  }

  .date {
    font-size: 15px;
  }
}

@media screen and (max-width: 1065px) {
  .image-container {
    width: 400px;
    height: 100%;
    margin-right: 0.75vw;
  }

  .image {
    width: 400px;
    height: 300px;
  }

  .title {
    font-size: 30px;
  }

  .description {
    font-size: 18px;
  }

  .content {
    font-size: 15px;
  }
}

@media screen and (max-width: 880px) {
  .image-container {
    width: 600px;
    height: 100%;
  }

  .image {
    width: 600px;
    height: 400px;
  }

  .text-container {
    width: 600px;
    float: left;
  }

  .title {
    font-size: 45px;
  }

  .description {
    font-size: 30px;
  }

  .content {
    font-size: 20px;
  }
}

@media screen and (max-width: 690px) {
  .image-container {
    width: 95%;
    height: 100%;
  }

  .image {
    width: 100%;
    height: auto;
  }

  .text-container {
    width: 95%;
    float: left;
  }

  .title {
    font-size: 6vw;;
  }

  .description {
    font-size: 4vw;
  }

  .content {
    font-size: 4vw;
  }
}

</style>
