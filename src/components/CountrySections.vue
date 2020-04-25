<template lang="html">
  <div class="overall-container">
  <div class="sections-container">
      <div  v-for="section in countrySections">
        <div class="sections">
          <a v-on:click="handleClick(section)">{{section}}</a>
        </div>
      </div>
  </div>
  </div>
</template>

<script>
import {eventBus} from '../main.js'

export default {
  name: 'country-sections',
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
    handleClick(section) {
      eventBus.$emit('selected-section', section)
    }
  },
}
</script>

<style lang="css" scoped>

.overall-container {
  width: 100vw;
  padding: 0;
  margin: 0;
  overflow: auto;
}

.sections-container {
  width: 98%;
  padding: 0;
  margin: 0;
  overflow: auto;
  padding-left: 5.5vw;
  display: flex;
}

.sections {
  float: left;
  color: #edf2f4;
  padding: 0;
  margin: 0;
  margin-right: 20px;
  margin-top: 15px;
  flex:1;
  font-family: 'Roboto', sans-serif;
}

.sections:hover {
  cursor: pointer;
}
</style>
