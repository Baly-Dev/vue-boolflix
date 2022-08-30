<template>
  <div id="app">
    <TheHeader/>
    <TheMain 
    :all="all" 
    :configBaseUrl="configBaseUrl" 
    :configImageSize="configImageSize"/>
  </div>
</template>

<script>
import axios from 'axios'
import TheHeader from './components/TheHeader.vue'
import TheMain from './components/TheMain.vue'
export default {
  name: 'App',
  data(){
    return{
      // API variables
      apiKey: '9d11cf0c498e7d3a362df8e3213bee33',
      apiSearchConfig:
      {
        moviePath: 'search/movie',
        showPath: 'search/tv',
        configPath: 'configuration',
        query: 'Star Wars'
      },
      movieURI: null,
      showURi: null,

      // Lists
      movies: [],
      shows: [],
      all: [],
      configBaseUrl: null,
      configImageSize: null
    }
  },
  created(){
    this.apiCall()
  },
  methods:{
    apiCall(){
      // movies call
      axios.get(this.generateMovieURI())
      .then(res => {
        this.movies = res.data.results

        this.movies.forEach(movie =>{
          this.all.push(movie)
        })
      })
      // shows call
      axios.get(this.generateShowURI())
      .then(res => {
        this.shows = res.data.results

        this.shows.forEach(show =>{
          this.all.push(show)
        })
      })

      // config call
      axios.get(this.generateConfigURI())
      .then(res => {
        this.configBaseUrl = res.data.images.base_url
        this.configImageSize = res.data.images.poster_sizes[3]
      })
    },
    generateMovieURI(){
      return `${this.apiSearchConfig.moviePath}?api_key=${this.apiKey}&query=${this.apiSearchConfig.query}`
    },
    generateShowURI(){
      return `${this.apiSearchConfig.showPath}?api_key=${this.apiKey}&query=${this.apiSearchConfig.query}`
    },
    generateConfigURI(){
      return `${this.apiSearchConfig.configPath}?api_key=${this.apiKey}`
    }
  },
  components: {
    TheMain,
    TheHeader
  }
}
</script>

<style lang="scss">
@import './assets/scss/global.scss';
</style>
