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
}

.sections-container {
  width: 98%;
  padding-left: 5.6vw;
  display: flex;
  flex-wrap: wrap;
}

.sections {
  float: left;
  color: #edf2f4;
  margin-right: 20px;
  margin-top: 20px;
  margin-bottom: 5px;
  font-family: 'Roboto', sans-serif;
}

.sections:hover {
  cursor: pointer;
  background-color: #edf2f4;
  color: #034078;
}

@media screen and (max-width: 490px) {
  .sections {
    margin-bottom: 0px;
    margin-top: 5px;
  }
}
</style>
