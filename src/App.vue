<template>
  <div class="wrapper">

    <Header @sendQuerySearch="querySearchFunction"/>

    <Main :resultsArray="resultsArray"/>
  
  </div>
</template>

<script>

import Header from './components/Header.vue'
import Main from './components/Main.vue'
import axios from 'axios'

export default {

  // mounted(){
  //  this.getApi();
  // },

  data(){
    return{
      resultsArray: [],
      apiKey: 'api_key=2773f939423c2a6dac0e7e805c296cf6&',
      filmserie: 'Film',
      querySearch: 'Braveheart',
      language: '&language=it_IT',
      page: '&page=1',
      apiURL: 'https://api.themoviedb.org/3/search/movie?',

    }
  },

  name: 'App',
  components: {
    Header,
    Main
  },

   
  methods:{
    getApi(){
      axios.get(`${this.apiURL}${this.apiKey}'&query='${this.querySearch}`)
      .then( r => {
        this.resultsArray = r.data.results;
        console.log(this.resultsArray);
      })
      .catch( e => {
        console.log(e);
      })
    },

      querySearchFunction(text){
      this.querySearch = text;
      console.log(this.querySearch);
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
