<template lang="html">
  <div>
    <section>
      <div class="overall-container">
        <div class="grid-container">
          <div class="grid">
            <news-articles v-for="article in randomArticles(randomIndex())" :article="article"><p>{{article.description}}</p></news-articles>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import NewsArticles from './NewsArticles.vue';

export default {
  name: 'news-list',
  props: ['articles'],
  components: {
    'news-articles': NewsArticles
  },
  methods: {
    randomArticles(index) {
      let articles = this.articles;
      let i, j, chunkedArray = [], chunk = 12;
      for (i=0, j=0; i < articles.length; i += chunk, j++) {
        chunkedArray[j] = articles.slice(i,i+chunk);
      }
      return chunkedArray[index];
    },
    randomIndex() {
      return Math.floor(Math.random() * 10)
    }
  }
}
</script>

<style lang="css" scoped>

.overall-container {
  display: block;
  text-align: center;
  margin-top: 20px;
}

.grid-container {
  width: 82%;
  display: inline-block;
}

.grid {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  text-align: center;
}

@media screen and (max-width: 1550px) {
  .grid-container {
  margin-left: 10%;
  }
}

@media screen and (max-width: 1350px) {
  .grid-container {
  margin-left: 5%;
  }
}

@media screen and (max-width: 1050px) {
  .grid-container {
  margin-left: 2.5%;
  }
}

@media screen and (max-width: 800px) {
  .grid-container {
  width: 95%;
  margin-left: 0%;
  }

  .overall-container {
    text-align: left;
  }
}


</style>
