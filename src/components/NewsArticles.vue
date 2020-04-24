<template lang="html">
  <div>
    {{article.title}}
    <a :href="article.url" target="_blank"><img :src="article.urlToImage"></a>
    <p>{{article.description}}</p>
  </div>
</template>

<script>
export default {
  name: 'news-articles',
  props: ['article']
}
</script>

<style lang="css" scoped>
</style>
