<template lang="html">
  <div>
    <div v-for="articles in processedArticles">
      <div v-for="article in articles">
        {{ article.title }}
        <a :href="article.url" target="_blank"><img :src="article.urlToImage"></a>
        <p>{{ article.description }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'news-list',
  props: ['results'],
  computed: {
    processedArticles() {
      let articles = this.results;

      let i, j, chunkedArray = [], chunk = 4;
      for (i=0, j=0; i < articles.length; i += chunk, j++) {
        chunkedArray[j] = articles.slice(i,i+chunk);
      }
      return chunkedArray;
    }
  }
}
</script>

<style lang="css" scoped>
</style>
