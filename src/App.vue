<template lang="html">
  <div>
    <section class="menu-container">
      <div class="logo-container">
        <img class="logo" :src="this.logoBlack">
      </div>
      <div class="form-container">
        <form>
          <select v-model="section">
            <option v-for="section in sections" :value="section">{{section}}</option>
          </select>
          <a v-on:click="getArticles(section)">Retrieve</a>
        </form>
      </div>
    </section>
    <section class="heading-container">
      <h1 class="heading">UK NEWS</h1>
    </section>
    <section>
      <top-stories :articles="articles"></top-stories>
    </section>
    <section>

    </section>
    <div>
      <news-list :articles="articles"></news-list>
    </div>
  </div>
</template>


<script>
import NewsList from './components/NewsList.vue';
import TopStories from './components/TopStories.vue';
import logoBlack from './assets/logo-black.png';
const axios = require('axios').default;
const QUERIES = "SCOTLAND, Aberdeen, Dumfries, Dundee, Edinburgh, Falkirk, Glasgow, Inverness, Perth, Stirling, ENGLAND, Bristol, Cambridge, Carlisle, Chester, Leeds, Leicester, Liverpool, London, Manchester, Newcastle, Norwich, Nottingham, Oxford, Portsmouth, Sheffield, Southampton, York, NORTHERN-IRELAND, Belfast, Derry, WALES, Bangor, Cardiff, Newport, Swansea";



export default {
  name: 'app',
  data() {
    return {
      articles: [],
      sections: QUERIES.split(', '),
      section: 'scotland',
      logoBlack: logoBlack
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
        this.articles = response.data.articles;
      });
    }
  },
  mounted() {
    this.getArticles('scotland');
  },
  components: {
    'news-list': NewsList,
    'top-stories': TopStories,
  }
}
</script>

<style lang="css" scoped>

.menu-container {
  width: 100vw;
  height: 40px;
  border-style: solid;
}

.logo-container {
  width: 4%;
  float: left;
  padding: 0;
  margin: 0;
}

.form-container {
  width: 15%;
  float: right;
  padding: 0;
  margin: 8px;
}

.heading-container {
  width: 100vw;
  height: 100px;
  border-style: solid;
  background-color: #034078;
}

.logo {
  height: 35px;
  padding-left: 5px;
  margin: 2px;
}

h1 {
  padding: 0;
  margin: 0;
  text-align: left;
  color: #edf2f4;
}

.heading {
  font-family: 'Exo 2', sans-serif;
  font-size: 30px;
}
</style>
