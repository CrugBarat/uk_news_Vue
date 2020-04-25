<template lang="html">
  <div>
    <div class="page-container">
      <div class="body-container">
        <section class="menu-container">
          <div class="logo-title-container">
            <div class="logo-container">
              <img class="logo" :src="this.logoBlack">
            </div>
            <div class="title-container">
              <h1 class="menu-title">UKN</h1>
            </div>
          </div>
          <div class="form-container">
            <div class="form">
            <form>
              <select v-model="section">
                <option v-for="section in sections" :value="section">{{section}}</option>
              </select>
              <a v-on:click="getArticles(section)">Retrieve</a>
            </form>
          </div>
        </div>
        </section>
      </div>
    </div>
    <section class="heading-container">
      <h1 class="heading">UK NEWS</h1>
      <menu-items :sections="sections"></menu-items>
    </section>
    <div class="page-container">
      <div class="body-container">
        <section>
          <top-stories :articles="articles"></top-stories>
        </section>
        <section>
        </section>
        <div>
          <news-list :articles="articles"></news-list>
        </div>
      </div>
    </div>
  </div>
</template>


<script>

import NewsList from './components/NewsList.vue';
import TopStories from './components/TopStories.vue';
import MenuItems from './components/MenuItems.vue';
import logoBlack from './assets/logo-black.png';
import {eventBus} from './main.js'

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
      const ApiKey = "3159bd64ef004f7584490af8761d30b0";
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

    eventBus.$on('selected-section', (section) => {
      this.getArticles(section);
    });

  },
  components: {
    'news-list': NewsList,
    'top-stories': TopStories,
    'menu-items': MenuItems,
  }
}
</script>

<style lang="css" scoped>

.page-container {
  width: 100vw;
}

.body-container {
  padding-left: 5vw;
  padding-right: 5vw;
}

.menu-container {
  height: 40px;
  overflow: auto;
}

.logo-title-container {
  float: left;
  width: 50%;
}

.logo-container {
  float: left;
  padding: 0;
  margin: 0;
}

.logo {
  height: 35px;
  padding-left: 5px;
  margin: 2px;
}

.menu-title {
  font-family: 'Exo 2', sans-serif;
  font-size: 30px;
  color: #202020;
  text-align: left;
}

.form-container {
  width: 45%;
  float: left;
  padding: 0;
  margin: 0;
  border-style: solid;
  overflow: auto;
}

.form {
  float: right;
  padding: 0;
  margin: 0;
  border-style: solid
}

.heading-container {
  width: 100%;
  height: 100px;
  background-color: #034078;
}

h1 {
  padding: 0;
  margin: 0;
}

.heading {
  font-family: 'Exo 2', sans-serif;
  font-size: 50px;
  width: 250px;
  margin-top: 0px;
  margin-left: 4vw;
  color: #edf2f4;
  text-align: center;
}



</style>
