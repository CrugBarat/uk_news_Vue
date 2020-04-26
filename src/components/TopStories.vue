<template lang="html">
  <div>
    <section>
        <div class="grid-container">
          <div class="grid">
            <top-stories-articles v-for="article in topArticles(randomIndex())" :article="article"></top-stories-articles>
          </div>
        </div>
    </section>
  </div>
</template>

<script>
import TopStoriesArticles from './TopStoriesArticles.vue';

export default {
  name: 'top-stories',
  props: ['articles'],
  components: {
    'top-stories-articles': TopStoriesArticles
  },
  methods: {
    topArticles(index) {
      let articles = this.articles;
      let i, j, chunkedArray = [], chunk = 3;
      for (i=0, j=0; i < articles.length; i += chunk, j++) {
        chunkedArray[j] = articles.slice(i,i+chunk);
      }
      return chunkedArray[index];
    },
    randomIndex() {
      return Math.floor(Math.random() * 30)
    }
  }
}
</script>

<style lang="css" scoped>

.grid-container {
  width: 100%;
  padding-top: 20px;
  padding-bottom: 10px;
  margin-left: 11%;
}

.grid {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  text-align: center;
}

@media screen and (max-width: 1500px) {
  .grid-container {
    margin-left: 0%;
  }
}


</style>
