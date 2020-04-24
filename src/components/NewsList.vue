<template lang="html">
  <div>
    <section>
      <news-articles v-for="article in this.articles" :article="article"></news-articles>
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
  }
}
</script>

<style lang="css" scoped>
</style>
