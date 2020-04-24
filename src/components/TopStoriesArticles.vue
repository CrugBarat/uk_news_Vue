<template lang="html">
  <div class="article">
    <a :href="article.url" target="_blank">
      <img class="article-image":src="article.urlToImage">
      <p class="title">{{article.title}}</p>
    </a>
  </div>
</template>

<script>
export default {
  name: 'top-stories-articles',
  props: ['article']
}
</script>

<style lang="css" scoped>

.article {
  border-style: solid;
  color: black;
  flex: 1, 0, auto;
  width: 32%;
}

a {
  text-decoration: none;
  color: inherit;
}

.article-image {
  width: 450px;
  height: 300px;
  padding: 0;
  margin: 0;
}

.title {
  padding: 0;
  margin: 0;
  font-family: 'Open Sans';
  font-size: 20px;
  font-weight: 700;
}
</style>
