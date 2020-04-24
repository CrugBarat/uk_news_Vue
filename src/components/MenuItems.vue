<template lang="html">
  <div class="sections-container">
      <div  v-for="section in countrySections">
        <div class="sections">
          <a v-on:click="handleClick">{{section}}</a>
        </div>
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

.sections-container {
  width: 100vw;
  padding: 0;
  margin: 0;
  overflow: auto;
  padding-left: 80px;
}

.sections {
  border-style: solid;
  border-color: transparent;
  float: left;
  clear: none;
  color: #edf2f4;
  padding: 0;
  margin: 0;
  margin-right: 20px;
  margin-top: 5px;
}

.sections:hover {
  cursor: pointer;
}
</style>
