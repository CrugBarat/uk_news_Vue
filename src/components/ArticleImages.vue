<template lang="html">
  <img :src="checkForImage">
</template>

<script>
import noImage from '../assets/noImage.png';

export default {
  name: 'article-images',
  props: ['imageUrl'],
  computed: {
    checkForImage(){
      return this.imageUrl != undefined ? this.imageUrl : noImage;
    }
  }
}
</script>

<style lang="css" scoped>

img {
  width: 390px;
  height: 300px;
  padding: 0;
  margin: 0;
}

</style>
