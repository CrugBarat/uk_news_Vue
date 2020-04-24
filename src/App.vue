<template lang="html">
  <div>
    <h1>UK NEWS</h1>
    <section>
      <h5>Filter by Category</h5>
      <form>
        <select v-model="section">
          <option v-for="section in sections" :value="section">{{section}}</option>
        </select>
        <a v-on:click="getArticles(section)">Retrieve</a>
      </form>
    </section>
    <div>
      <news-list :results="results"></news-list>
    </div>
  </div>
</template>


<script>
const QUERIES = "SCOTLAND, Aberdeen, Dumfries, Dundee, Edinburgh, Falkirk, Glasgow, Inverness, Perth, Stirling, ENGLAND, Bristol, Cambridge, Carlisle, Chester, Leeds, Leicester, Liverpool, London, Manchester, Newcastle, Norwich, Nottingham, Oxford, Portsmouth, Sheffield, Southampton, York, NORTHERN-IRELAND, Belfast, Derry, WALES, Bangor, Cardiff, Newport, Swansea";

import NewsList from './components/NewsList.vue'
export default {
  name: 'app',
  data() {
    return {
      results: [],
      sections: QUERIES.split(', '),
      section: 'scotland',
    }
  },
  methods: {
    buildUrl (url) {
      const NewsAPIBaseUrl = "https://newsapi.org/v2/everything?q=";
      const ApiKey = "7471aed1641e411b99a979fec157b562";
      return NewsAPIBaseUrl + url + "&apiKey=" + ApiKey
    },
    getArticles(section) {
      let url = this.buildUrl(section);
      axios.get(url).then((response) => {
        this.results = response.data.articles;
      });
    }
  },
  mounted() {
    this.getArticles('scotland');
  },
  components: {
    'news-list': NewsList
  }
}
</script>

<style lang="css" scoped>
</style>
