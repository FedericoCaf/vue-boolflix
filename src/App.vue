<template>
  <div class="wrapper">

    <Header @sendQuerySearch="querySearchFunction"/>

    <Main :arrayConcat="arrayConcat" />
   
  </div>
</template>

<script>

import Header from './components/Header.vue'
import Main from './components/Main.vue'
import axios from 'axios'

export default {

  data(){
    return{
      arrayMovie: [],
      arrayTv: [],
      arrayConcat: [],
      apiKey:'api_key=2773f939423c2a6dac0e7e805c296cf6&',

      querySearch: '',
      language: '&language=it_IT',
      page: '&page=1',
      apiURLmovie:'https://api.themoviedb.org/3/search/movie?',
      apiURLtv:'https://api.themoviedb.org/3/search/tv?',
    }
  },

  name: 'App',
  components: {
    Header,
    Main
  },

  methods:{

    getApi(array1, array2){
      axios.get(`${this.apiURLmovie}${this.apiKey}'&query='${this.querySearch}`)
      .then( r => {
        array1 = r.data.results;
        this.arrayConcat = array1.concat(array2);
      })
      .catch( e => {
        console.log(e);
      })

      axios.get(`${this.apiURLtv}${this.apiKey}'&query='${this.querySearch}`)
      .then( resp => {
        array2 = resp.data.results;
        this.arrayConcat = array1.concat(array2);

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
       this.getApi(this.arrayMovie, this.arrayTv);
    }

  }
}

</script>

<style lang="scss">

 @import "./assets/style/vars.scss";
 @import "./assets/style/generals.scss";
 @import "./assets/style/utilities.scss";

</style>
