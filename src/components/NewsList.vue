<template lang="html">
  <div>
    <section>
      <div class="overall-container">
        <div class="grid-container">
          <div class="grid">
            <news-articles v-for="article in this.articles" :article="article"><p>{{article.description}}</p></news-articles>
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
  }
}
</script>

<style lang="css" scoped>

.overall-container {
  display: block;
  text-align: center;
}

.grid-container {
  display: inline-block;
}

.grid {
  border-style: solid;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  color: pink;
}

</style>
