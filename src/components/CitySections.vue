<template lang="html">
  <div class="overall-container">
  <div class="sections-container">
      <div  v-for="section in citySections">
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
  name: 'city-sections',
  props: ['sections'],
  computed: {
    citySections() {
      return this.sections.filter(city => {
        return city !== 'SCOTLAND' && city !== 'ENGLAND'
        && city !== 'WALES' && city !== 'NORTHERN-IRELAND'
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
}

.sections-container {
  width: 98%;
  padding: 0;
  margin: 0;
  padding-left: .6vw;
  display: flex;
  flex-wrap: wrap;
}

.sections {
  float: left;
  color: #202020;
  margin-right: 1.5vw;
  margin-top: 5px;
  font-family: 'Roboto', sans-serif;
}

.sections:hover {
  cursor: pointer;
  background-color: #034078;
  color: #edf2f4;
}
</style>
