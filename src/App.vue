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
    <section class="heading-container">
      <h1 class="heading">COVID-19 UPDATE</h1>
      <div class="overall-covid-container">
        <div class="covid-container">
          <div v-for="country in countries">
            <div class="covid-countries">
              <a v-on:click="handleCountryClick(country)">{{country.toUpperCase()}}</a>
            </div>
          </div>
        </div>
      </div>
    </section>
    <div class="page-container">
      <div class="main-container">
        <section>
          <div class="covid-queries-container">
            <div v-for="query in queryTypes">
              <div class="covid-queries">
                <a v-on:click="handleQueryClick(query)">{{query.toUpperCase()}}</a>
              </div>
            </div>
          </div>
        </section>
        <section>
          <div class="chart">
            <covid-chart :covidData="covidData"></covid-chart>
          </div>
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
  import CovidChart from "@/components/CovidChart.vue";
  import {map, sumBy, flatten, groupBy} from "lodash";
  import {eventBus} from './main.js'

  const axios = require('axios').default;
  const SECTIONS = "SCOTLAND, Glasgow, Edinburgh, ENGLAND, Liverpool, London, Manchester, Newcastle, NORTHERN-IRELAND, WALES, Cardiff";
  const SPORTSSECTIONS = "FOOTBALL, RUGBY, CRICKET";
  const COUNTRIES = "united-kingdom, france, germany, spain, italy, russia, united-states, china";
  const QUERIES = "Confirmed, Active, Recovered, Deaths";

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
        covidData: null,
        countries: COUNTRIES.split(', '),
        country: 'united-kingdom',
        queryTypes: QUERIES.split(', '),
        queryType: 'Confirmed',
      }
    },
    methods: {
      buildUrl(section) {
        const NewsAPIBaseUrl = "https://newsapi.org/v2/everything?q=";
        const domains = "bbc.co.uk, dailymail.co.uk, dailyrecord.co.uk, metro.co.uk, thesun.co.uk, theguardian.com, express.co.uk, news.google.com, news.yahoo.com"
        const date = "2020-04-12"
        const ApiKey = "b325bdb5ffa64154995253c137e4d682";
        return NewsAPIBaseUrl + section + "&domains=" + domains + "&from=" + date + "&language=en&pageSize=100&apiKey=" + ApiKey
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
      },
      buildCVUrl(country) {
        const CVBaseUrl = "https://api.covid19api.com/live/country/";
        const date = "2020-03-17T00:00:00Z"
        return CVBaseUrl + country + "/status/confirmed/date/" + date
      },
      getCVData(country, queryType) {
        let url = this.buildCVUrl(country);
        axios.get(url).then((response) => {
          const covidData = response.data;
          const flattenedCovidData = flatten(covidData);
          const groupedCovidData = groupBy(flattenedCovidData, 'Date');

          const sortedCovidData = map(groupedCovidData, (array, date) => {
            const getQuery = sumBy(array, queryType);
            return {'Date': date, 'Query': getQuery}
          })
          this.covidData = sortedCovidData;
        });
      },
      handleCountryClick(country) {
        this.country = country;
      },
      handleQueryClick(query) {
        this.getCVData(this.country, query)
      }
    },
    mounted() {
      this.getArticles('scotland');
      this.getSportsArticles('sports');

      eventBus.$on('selected-section', (section) => {
        this.getArticles(section);
      });

      eventBus.$on('selected-sports-section', (section) => {
        this.getSportsArticles(section);
      });

      this.getCVData('united-kingdom', 'Confirmed')

    },
    components: {
      'news-list': NewsList,
      'top-stories': TopStories,
      'country-sections': CountrySections,
      'city-sections': CitySections,
      'sports-sections': SportSections,
      'hero-article': HeroArticle,
      'covid-chart': CovidChart,
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
    height: 15px;
    font-family: 'Roboto', sans-serif;
    font-size: 15px;
    border-color: #034078;
  }

  input, .search-image:focus {
    outline: none;
  }

  input {
    height: 15px;
  }

  .heading-container {
    width: 100vw;
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
    height: 50px;
    background-color: #034078;
  }

  .chart {
    width: 95%;
    min-height: 450px;
    margin: 1vw;
    overflow: auto
  }

  .overall-covid-container {
    width: 100vw;
  }

  .covid-container {
    width: 98%;
    padding-left: 5.6vw;
    display: flex;
    flex-wrap: wrap;
  }

  .covid-countries {
    float: left;
    color: #edf2f4;
    margin-right: 20px;
    margin-top: 20px;
    margin-bottom: 5px;
    font-family: 'Roboto', sans-serif;
  }

  .covid-countries:hover {
    cursor: pointer;
    background-color: #edf2f4;
    color: #034078;
  }

  .covid-queries-container {
    width: 98%;
    padding-left: 0.8vw;
    display: flex;
    flex-wrap: wrap;
  }

  .covid-queries {
    float: left;
    color: #202020;
    margin-right: 1.5vw;
    margin-top: 5px;
    font-family: 'Roboto', sans-serif;
  }

  .covid-queries:hover {
    cursor: pointer;
    background-color: #034078;
    color: #edf2f4;
  }


  @media screen and (max-width: 620px) {
    .logo-title-container {
      width: 30%;
    }

    .search-container {
      width: 70%;
    }

    .covid-countries {
      margin-bottom: 0px;
      margin-top: 5px;
    }
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

a:hover {
  text-decoration: underline;
  color: #034078;
}
</style>
