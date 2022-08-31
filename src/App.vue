<template>
  <div id="app">
    <TheHeader @emitSearch="getSearchParameter"/>
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
      query: '',
      flagCode:'',

      // Lists
      movies: [],
      shows: [],
      all: [],
      configBaseUrl: null,
      configImageSize: null,
    }
  },
  methods:{
    apiCall(){
      // movies call
      axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${this.apiKey}&query=${this.query}&language=it-IT`)
      .then(res => {
        this.movies = res.data.results
        this.movies.forEach(movie =>{
          this.all.push(movie)
        })
      })
      .catch(err => {
        console.log(err)
      })

      // shows call
      axios.get(`https://api.themoviedb.org/3/search/tv?api_key=${this.apiKey}&query=${this.query}&language=it-IT`)
      .then(res => {
        this.shows = res.data.results
        this.shows.forEach(show =>{
          this.all.push(show)
        })
      })
      .catch(err => {
        console.log(err)
      })

      // config call
      axios.get(`https://api.themoviedb.org/3/configuration?api_key=${this.apiKey}`)
      .then(res => {
        this.configBaseUrl = res.data.images.base_url
        this.configImageSize = res.data.images.poster_sizes[3]
      })
      .catch(err => {
        console.log(err)
      })

      // languages flag call
    },
    getSearchParameter(parameter){
      this.query = parameter
      this.apiCall()

      

    },
    getFlags(){

      
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
