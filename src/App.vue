<template>
  <div id="app">
    <TheHeader @emitSearch="getSearchParameter"/>
    <TheMain 
    :movies="movies"
    :shows="shows"
    :configBaseUrl="configBaseUrl" 
    :configImageSize="configImageSize"/>
    <TheFooter 
    :moviesPages="moviesPages"
    :showsPages="showsPages"
    @nextPage="getNextPage"
    @prevPage="getPrevPage"
    />
  </div>
</template>

<script>
import axios from 'axios'
import TheHeader from './components/TheHeader.vue'
import TheMain from './components/TheMain.vue'
import TheFooter from './components/TheFooter.vue'
export default {
  name: 'App',
  data(){
    return{
      // API variables
      apiKey: '9d11cf0c498e7d3a362df8e3213bee33',
      query: '',

      // Lists
      movies: [],
      shows: [],
      moviesPages: {},
      showsPages: {},
      currentPage: 1,
      configBaseUrl: null,
      configImageSize: null
    }
  },
  methods:{
    apiCall(){
      axios.defaults.baseURL = 'https://api.themoviedb.org/3/'
      const apiParams = {
        api_key: this.apiKey,
        language: 'it-It',
        query: this.query, 
        page: this.currentPage
      }

      this.getMovieApi(apiParams)
      this.getShowApi(apiParams)
      this.getConfigApi()
    },
    getMovieApi(par){
      // movies search call
      axios.get('search/movie', {params:par})
      .then(res => {

        // getting data
        this.moviesPages = res.data
        this.movies = res.data.results

        this.movies.forEach(movie =>{
          // chekin ISO mismatch
          this.checkLanguage(movie)
          movie.type = 'movie'
        })
      })
      .catch(err => {
        console.log(err)
      })
    },
    getShowApi(par){
      // shows search call
      axios.get('search/tv', {params:par})
      .then(res => {

        // getting data
        this.showsPages = res.data
        this.shows = res.data.results

        this.shows.forEach(show =>{
          // chekin ISO mismatch
          this.checkLanguage(show)
          show.type = 'show'
        })
      })
      .catch(err => {
        console.log(err)
      })
    },
    getConfigApi(){
      // config call
      axios.get(`configuration?api_key=${this.apiKey}`)
      .then(res => {
        this.configBaseUrl = res.data.images.base_url
        this.configImageSize = res.data.images.poster_sizes[3]
      })
      .catch(err => {
        console.log(err)
      })
    },
    getSearchParameter(parameter){
      this.movies = []
      this.shows = []
      this.query = parameter
      this.apiCall()
    },
    getNextPage(parameter){
      this.movies = []
      this.shows = []
      this.currentPage = parameter
      this.apiCall()
    },
    getPrevPage(parameter){
      this.movies = []
      this.shows = []
      this.currentPage = parameter
      this.apiCall()
    },
    checkLanguage(type){
      if (type.original_language == ''){
        type.original_language = 'n/a'
      }

      if (type.original_language == 'en'){
        type.original_language = 'gb'
      }

      if (type.original_language == 'ja'){
        type.original_language = 'jp'
      }

      if (type.original_language == 'zh'){
        type.original_language = 'cn'
      }
    }
  },
  components: {
    TheMain,
    TheHeader,
    TheFooter
  }
}
</script>

<style lang="scss">
@import './assets/scss/global.scss';
</style>
