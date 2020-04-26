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
          <div class="search-container">
            <div class="search">
              <form>
                <input class="search-box" type="text" v-model="searchNews">
                <input class="search-logo" type="image" :src="searchIcon" v-on:click.prevent="handleSearch"></input>
              </form>
            </div>
          </div>
        </section>
      </div>
    </div>
    <section class="heading-container">
      <h1 class="heading">UK NEWS</h1>
      <country-sections :sections="sections"></country-sections>
    </section>
    <div class="page-container">
      <div class="body-container">
        <section>
          <city-sections :sections="sections"></city-sections>
        </section>
        <section>
          <top-stories :articles="articles"></top-stories>
          <hr>
        </section>
        <section>
          <hero-article :articles="articles"></hero-article>
          <hr>
        </section>
        <section>
          <top-stories :articles="articles"></top-stories>
          <hr>
        </section>
        <section>
          <hero-article :articles="articles"></hero-article>
          <hr>
        </section>
        <section>
          <div>
            <news-list :articles="articles"></news-list>
          </div>
        </section>
        <section>
          <top-stories :articles="articles"></top-stories>
          <hr>
        </section>
      </div>
    </div>
    <section class="heading-container">
      <h1 class="heading">SPORTS</h1>
      <!-- <country-sections :sections="sections"></country-sections> -->
    </section>
    <div class="page-container">
      <div class="body-container">
        <section>
          <top-stories :articles="articles"></top-stories>
          <hr>
        </section>
        <section>
          <hero-article :articles="articles"></hero-article>
          <hr>
        </section>
        <section>
          <div>
            <news-list :articles="articles"></news-list>
          </div>
        </section>
        <section>
          <top-stories :articles="articles"></top-stories>
          <hr>
        </section>
      </div>
    </div>
    <section>
      <div class="footer"></div>
    </section>
  </div>
</template>


<script>

import NewsList from './components/NewsList.vue';
import TopStories from './components/TopStories.vue';
import CountrySections from './components/CountrySections.vue';
import CitySections from './components/CitySections.vue';
import HeroArticle from './components/HeroArticle.vue';
import logoBlack from './assets/logo-black.png';
import searchIcon from './assets/search.png';
import {eventBus} from './main.js'

const axios = require('axios').default;
const QUERIES = "SCOTLAND, Aberdeen, Edinburgh, Glasgow, ENGLAND, Liverpool, London, Manchester, Newcastle, NORTHERN-IRELAND, Belfast, WALES, Cardiff, Swansea";



export default {
  name: 'app',
  data() {
    return {
      articles: [],
      sections: QUERIES.split(', '),
      section: 'scotland',
      logoBlack: logoBlack,
      searchIcon: searchIcon,
      searchNews: "",
    }
  },
  methods: {
    buildUrl (url) {
      const NewsAPIBaseUrl = "https://newsapi.org/v2/everything?q=";
      const ApiKey = "3159bd64ef004f7584490af8761d30b0";
      return NewsAPIBaseUrl + url + "&pageSize=100&apiKey=" + ApiKey
    },
    getArticles(section) {
      let url = this.buildUrl(section);
      axios.get(url).then((response) => {
        this.articles = response.data.articles;
      });
    },
    handleSearch(){
      this.getArticles(this.searchNews)
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
    'country-sections': CountrySections,
    'city-sections': CitySections,
    'hero-article': HeroArticle,
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

.search-container {
  width: 45%;
  float: left;
  padding: 0;
  margin: 0;
  overflow: auto;
}

.search {
  float: right;
  padding: 0;
  margin: 5px;
}

.search-logo {
  padding-left: 5px;
}

.search-box {
  width: 200px;
  font-family: 'Roboto', sans-serif;
  font-size: 20px;
}

input, .search-image:focus {
  outline: none;
}

input {
  height: 15px;
}

.heading-container {
  width: 100%;
  height: 110px;
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
  margin-left: 4.5vw;
  color: #edf2f4;
  text-align: center;
}

.footer {
  width: 100%;
  height: 100px;
  background-color: #034078;
}

</style>

<style>
body {
  overflow-x: hidden;
  user-select: none;
  background-color: #edf2f4;
}
</style>
