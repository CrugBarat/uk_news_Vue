<template lang="html">
  <div class="overall-container">
  <div class="sections-container">
      <div  v-for="section in sections">
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
  name: 'sport-sections',
  props: ['sections'],
  methods: {
    handleClick(section) {
      eventBus.$emit('selected-sports-section', section)
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
  margin-top: 20px;
  flex:1;
  font-family: 'Roboto', sans-serif;
}

.sections:hover {
  cursor: pointer;
  background-color: #edf2f4;
  color: #034078;
}
</style>
