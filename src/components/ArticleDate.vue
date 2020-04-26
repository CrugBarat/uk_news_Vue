<template lang="html">
  <p class="date">{{formatDate}}</p>
</template>

<script>
export default {
  name: 'article-date',
  props: ['publishedAt'],
  computed: {
    formatDate () {
      const date = new Date (this.publishedAt);
      const dtf = new Intl.DateTimeFormat('en', {year: 'numeric', month: 'long', day: '2-digit'})
      const [{value: month },,{value: day},,{value: year}] = dtf.formatToParts(date)
      return `${day} ${month} ${year}`
    }
  }
}

</script>

<style lang="css" scoped>
.date {
  font-weight: bold;
}
</style>
