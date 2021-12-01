<template>
  <div class="wrapper">

    <Header/>

    <Main :resultsArray="resultsArray"/>
  
  </div>
</template>

<script>

import Header from './components/Header.vue'
import Main from './components/Main.vue'
import axios from 'axios'

export default {

  mounted(){
   this.getApi();
  },

  data(){
    return{
      resultsArray: [],
      apiURL: 'https://api.themoviedb.org/3/search/movie?api_key=2773f939423c2a6dac0e7e805c296cf6&query=braveheart',

    }
  },

  name: 'App',
  components: {
    Header,
    Main
  },

  methods:{
    getApi(){
      axios.get(this.apiURL)
      .then( r => {
        this.resultsArray = r.data.results;
        console.log(this.resultsArray);
      })
      .catch( e => {
        console.log(e);
      })
    },
  }
}


</script>

<style lang="scss">

 @import "./assets/style/vars.scss";
 @import "./assets/style/generals.scss";
 @import "./assets/style/utilities.scss";

</style>
