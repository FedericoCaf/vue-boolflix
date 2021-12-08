<template>
  <div class="wrapper">

    <Header @sendQuerySearch="querySearchFunction"/>

    <Main :arrayConcat="arrayConcat" :arrayTrend="arrayTrend" :arrayMovie="arrayMovie" :arrayTv="arrayTv"     :arrayRecommended="arrayRecommended" :arrayTop="arrayTop" :searchClicked="searchClicked" :arrayTvPop="arrayTvPop" />
   
  </div>
</template>

<script>

import Header from './components/Header.vue'
import Main from './components/Main.vue'
import axios from 'axios'

export default {

  data(){
    return{
      searchClicked:false,
      arrayTrend: [],
      arrayMovie: [],
      arrayTv: [],
      arrayConcat: [],
      arrayRecommended: [],
      arrayTop: [],
      arrayTvPop: [],

      apiKey:'api_key=2773f939423c2a6dac0e7e805c296cf6&',

      querySearch: 'Terminator',
      language: '&language=it_IT',
      page: '&page=1',
      apiURLtrend: 'https://api.themoviedb.org/3/trending/all/week?',
      apiURLmovie:'https://api.themoviedb.org/3/search/movie?',
      apiURLtv:'https://api.themoviedb.org/3/search/tv?',
      apiURLrecommended: 'https://api.themoviedb.org/3/movie/105/recommendations?',
      apiURLtop: 'https://api.themoviedb.org/3/movie/top_rated?',
      apiURLtvPop: 'https://api.themoviedb.org/3/tv/popular?'
    }
  },

  name: 'App',
  components: {
    Header,
    Main
  },

   mounted(){
      this.getHome();
    },

  methods:{

    getHome(){
       axios.get(`${this.apiURLtrend}${this.apiKey}`)
      .then( response => {
        this.arrayTrend = response.data.results;
       
      })
      .catch( e => {
        console.log(e);
      })
       axios.get(`${this.apiURLrecommended}${this.apiKey}`)
      .then( response => {
        this.arrayRecommended = response.data.results;
      
      })
      .catch( e => {
        console.log(e);
      })
       axios.get(`${this.apiURLtop}${this.apiKey}`)
      .then( response => {
        this.arrayTop = response.data.results;
       
      })
      .catch( e => {
        console.log(e);
      })
       axios.get(`${this.apiURLtvPop}${this.apiKey}`)
      .then( response => {
        this.arrayTvPop = response.data.results;
       
      })
      .catch( e => {
        console.log(e);
      })


    },

    getApi(){
      // axios.get(`${this.apiURLtrend}${this.apiKey}`)
      // .then( response => {
      //   this.arrayTrend = response.data.results;
      //   // this.arrayConcat = array1.concat(array2);
      // })
      // .catch( e => {
      //   console.log(e);
      // })

      axios.get(`${this.apiURLmovie}${this.apiKey}'&query='${this.querySearch}`)
      .then( r => {
        this.arrayMovie = r.data.results;
        // this.arrayConcat = array1.concat(array2);
      })
      .catch( e => {
        console.log(e);
      })

      axios.get(`${this.apiURLtv}${this.apiKey}'&query='${this.querySearch}`)
      .then( resp => {
        this.arrayTv = resp.data.results;
        // this.arrayConcat = array1.concat(array2);
      })
      .catch( e => {
        console.log(e);
      })
        console.log('search query',this.querySearch);
        console.log('array film',this.arrayMovie);
        console.log('array tv',this.arrayTv);
        console.log('array concatenato', this.arrayConcat);
    },

      querySearchFunction(text){
       this.querySearch = text;
       this.searchClicked = true;
       this.getApi();
    }

  }
}

</script>

<style lang="scss">

 @import "./assets/style/vars.scss";
 @import "./assets/style/generals.scss";
 @import "./assets/style/utilities.scss";


</style>
