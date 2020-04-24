<template lang="html">
  <div>
    <section>
      <div v-for="article in topArticles">
        {{article.title}}
        <a :href="article.url" target="_blank"><img :src="article.urlToImage"></a>
        <p>{{article.description}}</p>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: 'top-stories',
  props: ['articles'],
  computed: {
    topArticles() {
      let articles = this.articles
        let i, j, chunkedArray = [], chunk = 4;
        for (i=0, j=0; i < articles.length; i += chunk, j++) {
          chunkedArray[j] = articles.slice(i,i+chunk);
        }
        return chunkedArray[0];
      }
    }
  }
</script>

<style lang="css" scoped>
</style>
