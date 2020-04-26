<template lang="html">
  <p :value="handleDate">{{handleDate}}</p>
</template>

<script>
export default {
  name: 'article-date',
  props: ['publishedAt'],
  computed: {
    handleDate () {
      const date = new Date (this.publishedAt);
      const dtf = new Intl.DateTimeFormat('en', {year: 'numeric', month: 'long', day: '2-digit'})
      const [{value: month },,{value: day},,{value: year}] = dtf.formatToParts(date)
      return `${day} ${month} ${year}`
    }
  }
}

</script>

<style lang="css" scoped>
</style>
