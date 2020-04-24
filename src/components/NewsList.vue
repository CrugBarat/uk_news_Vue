<template lang="html">
  <div>
    <section>
      <div v-for="article in this.articles">
        {{article.title}}
        <a :href="article.url" target="_blank"><img :src="article.urlToImage"></a>
        <p>{{article.description}}</p>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: 'news-list',
  props: ['articles'],
}
</script>

<style lang="css" scoped>
</style>
