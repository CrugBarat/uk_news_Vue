<template lang="html">
  <img :src="checkForImage">
</template>

<script>
import noImage from '../assets/noImage.jpg';

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

@media screen and (max-width: 1400px) {
  img {
    width: 350px;
    height: 260px;
  }
}

@media screen and (max-width: 1230px) {
  img {
    width: 300px;
    height: 210px;
  }
}

@media screen and (max-width: 1060px) {
  img {
    width: 250px;
    height: 160px;
  }
}

@media screen and (max-width: 880px) {
  img {
    width: 600px;
    height: 400px;
  }
}

@media screen and (max-width: 670px) {
  img {
    width: 400px;
    height: 300px;
  }
}

@media screen and (max-width: 460px) {
  img {
    width: 250px;
    height: 160px;
  }
}

@media screen and (max-width: 350px) {
  img {
    width: 86vw;
    height: 200px;
  }
}

</style>
