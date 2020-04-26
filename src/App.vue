<template lang="html">
  <div>
    <div class="page-container">
      <div class="main-container">
        <section>
          <div class="logo-title-container">
            <div class="logo-container">
              <img class="logo" :src="this.logoBlack">
            </div>
            <div>
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
      <div class="main-container">
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
            <hr>
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
      <sports-sections :sections="sportsSections"></sports-sections>
    </section>
    <div class="page-container">
      <div class="main-container">
        <section>
          <top-stories :articles="sportsArticles"></top-stories>
          <hr>
        </section>
        <section>
          <hero-article :articles="sportsArticles"></hero-article>
          <hr>
        </section>
        <section>
          <div>
            <news-list :articles="sportsArticles"></news-list>
            <hr>
          </div>
        </section>
        <section>
          <top-stories :articles="sportsArticles"></top-stories>
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
import SportSections from './components/SportSections.vue';
import HeroArticle from './components/HeroArticle.vue';
import logoBlack from './assets/logo-black.png';
import searchIcon from './assets/search.png';
import {eventBus} from './main.js'

const axios = require('axios').default;
const SECTIONS = "SCOTLAND, Aberdeen, Edinburgh, Glasgow, ENGLAND, Liverpool, London, Manchester, Newcastle, NORTHERN-IRELAND, Belfast, WALES, Cardiff, Swansea";
const SPORTSSECTIONS = "FOOTBALL, RUGBY, CRICKET";



export default {
  name: 'app',
  data() {
    return {
      articles: [],
      sportsArticles: [],
      sections: SECTIONS.split(', '),
      section: 'scotland',
      sportsSections: SPORTSSECTIONS.split(', '),
      sportSection: 'sports',
      logoBlack: logoBlack,
      searchIcon: searchIcon,
      searchNews: "",
    }
  },
  methods: {
    buildUrl(section) {
      const NewsAPIBaseUrl = "https://newsapi.org/v2/everything?q=";
      const domains = "bbc.co.uk, dailymail.co.uk, dailyrecord.co.uk, metro.co.uk, thesun.co.uk, theguardian.com, express.co.uk, news.google.com, news.yahoo.com"
      const ApiKey = "3159bd64ef004f7584490af8761d30b0";
      return NewsAPIBaseUrl + section + "&domains=" + domains + "&language=en&pageSize=100&apiKey=" + ApiKey
    },
    getArticles(section) {
      let url = this.buildUrl(section);
      axios.get(url).then((response) => {
        this.articles = response.data.articles;
      });
    },
    getSportsArticles(section) {
      let url = this.buildUrl(section);
      axios.get(url).then((response) => {
        this.sportsArticles = response.data.articles;
      });
    },
    handleSearch(){
      this.getArticles(this.searchNews)
    }
  },
  mounted() {
    // this.getArticles('scotland');
    // this.getSportsArticles('sports');

    eventBus.$on('selected-section', (section) => {
      this.getArticles(section);
    });

    eventBus.$on('selected-sports-section', (section) => {
      this.getSportsArticles(section);
    });

  },
  components: {
    'news-list': NewsList,
    'top-stories': TopStories,
    'country-sections': CountrySections,
    'city-sections': CitySections,
    'sports-sections': SportSections,
    'hero-article': HeroArticle,
  }
}
</script>

<style lang="css" scoped>

.page-container {
  width: 100vw;
}

.main-container {
  padding-left: 5vw;
  padding-right: 5vw;
}

.logo-title-container {
  float: left;
  width: 50%;
}

.logo-container {
  float: left;
}

.logo {
  height: 25px;
  padding-left: 5px;
  margin: 2px;
}

.menu-title {
  font-family: 'Exo 2', sans-serif;
  font-size: 25px;
  color: #202020;
  text-align: left;
}

.search-container {
  width: 45%;
  padding: 0;
  overflow: auto;
}

.search {
  float: right;
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
  width: 100vw;
  /* height: 110px; */
  background-color: #034078;
}

h1 {
  padding: 0;
  margin: 0;
}

.heading {
  font-family: 'Exo 2', sans-serif;
  font-size: 50px;
  margin-left: 5.4vw;
  padding-top: 5px;
  color: #edf2f4;
  text-align: left;
}

.footer {
  width: 100vw;
  height: 100px;
  background-color: #034078;
}

@media screen and (max-width: 620px) {
  .logo-title-container {
    width: 30%;
  }

  .search-container {
    width: 70%;
  }

  /* .search-box {
    width: 150px;
  } */
}

@media screen and (max-width: 490px) {
  .logo-title-container {
    float: none;
    width: 100%;
  }

  .search-container {
    width: 100%;
  }

  .search {
    float: none;
  }

}

</style>

<style>
body {
  user-select: none;
  background-color: #edf2f4;
  overflow-x: hidden;
  width: 100vw;
}
</style>
