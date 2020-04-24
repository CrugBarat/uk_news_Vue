<template lang="html">
  <div>
    <section>
      <news-articles v-for="article in topArticles(randomIndex())" :article="article"></news-articles>
    </section>
  </div>
</template>

<script>
import NewsArticles from './NewsArticles.vue';

export default {
  name: 'top-stories',
  props: ['articles'],
  components: {
    'news-articles': NewsArticles
  },
  methods: {
    topArticles(index) {
      let articles = this.articles;
      let i, j, chunkedArray = [], chunk = 4;
      for (i=0, j=0; i < articles.length; i += chunk, j++) {
        chunkedArray[j] = articles.slice(i,i+chunk);
      }
      return chunkedArray[index];
    },
    randomIndex() {
      return Math.floor(Math.random() * 3)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
