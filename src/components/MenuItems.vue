<template lang="html">
  <div>
    <div v-for="section in countrySections">
      <a v-on:click="handleClick">{{section}}</a>
    </div>
  </div>
</template>

<script>
import {eventBus} from '../main.js'

export default {
  name: 'menu-items',
  props: ['sections'],
  computed: {
    countrySections() {
      return this.sections.filter(country => {
        return country === 'SCOTLAND' || country === 'ENGLAND'
         || country === 'WALES' || country === 'NORTHERN-IRELAND'
      });
      }
    },
  methods: {
    handleClick() {
      eventBus.$emit('selected-section', this.section)
    }
  },
}
</script>

<style lang="css" scoped>
</style>
