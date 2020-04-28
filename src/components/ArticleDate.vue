<template lang="html">
  <p class="date">{{formatDate}}</p>
</template>

<script>
import moment from 'moment';

export default {
  name: 'article-date',
  props: ['publishedAt'],
  computed: {
    formatDate () {
      return moment(this.publishedAt).format('DD MMM YYYY')
    }
  }
}

</script>

<style lang="css" scoped>
.date {
  font-weight: bold;
}
</style>
