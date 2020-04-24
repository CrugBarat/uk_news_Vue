<template lang="html">
  <div>
    <section>
      <div v-for="article in topArticles(randomIndex())">
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
