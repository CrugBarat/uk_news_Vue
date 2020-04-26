<template lang="html">
  <div>
    <section>
      <div class="overall-container">
        <div class="grid-container">
          <div class="grid">
            <top-stories-articles v-for="article in topArticles(randomIndex())" :article="article"></top-stories-articles>
          </div>
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
      return Math.floor(Math.random() * 33)
    }
  }
}
</script>

<style lang="css" scoped>

.overall-container {
  display: block;
  text-align: center;
  padding-top: 20px;
}

.grid-container {
  width: 100%;
  padding: 0;
  margin: 0;
  display: inline-block;
}

.grid {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  text-align: center;
}

</style>
