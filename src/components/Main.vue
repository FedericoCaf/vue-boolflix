<template>
 <main>
  <!-- <div class="global-title fc-container">
   <select @change="switchSelect($event)">
     <option selected value="0">Tutto</option>
     <option value="1">Film</option>
     <option value="2">Serie Tv</option>
   </select>
  </div> -->

    <div  v-if="!searchClicked"  class="global-card">
     <vue-custom-scrollbar class="scroll-area"  :settings="settings" @ps-scroll-y="scrollHanle">      
        <div class="title-genr fc-flex fc-align-center"> <h2> TITOLI DI TENDENZA </h2> </div>
      
      <div class="container-card fc-flex">
        
        <!-- <p> {{this.filteredCards[activeFilm].id}} </p> -->
        <div v-for="(item, index) in arrayTrend" :key="item.id" class="card">
            <div class="card-img">

              <img v-if="item.poster_path !== null " :src="'http://image.tmdb.org/t/p/w300' + item.poster_path" alt="">
              <div v-else class="card fc-flex fc-align-center fc-justify-center">
                <h2 v-if="item.hasOwnProperty('title')"> {{item.title}} </h2>
                <h2 v-if="item.hasOwnProperty('name')"> {{item.name}} </h2>
              </div>
            </div>

            <div class="card-text">
              <div class="container-title">
                <h2 v-if="item.hasOwnProperty('title')"> {{item.title}} </h2>
                <h2 v-if="item.hasOwnProperty('name')"> {{item.name}} </h2>
              </div>
      
              <ul>
                <div class="content-card-top">
                    <li v-if="item.hasOwnProperty('original_title')"> Titolo originale: {{item.original_title}} </li>
                    <li v-if="item.hasOwnProperty('original_name')"> Titolo originale: {{item.original_name}} </li>
                    <li>
                        Lingua: 
                        <img 
                          class="language" 
                          v-if="langFunction(item) !== ''" :src="langFunction(item)" :alt="item.original_language"
                        >
                        <span v-else>{{ item.original_language }}</span>

                    </li>
                    <li> 
                        <i v-for="(star, index) in 5" :key="index" class="fa-star"  
                          :class="index < Math.round(item.vote_average / 2 ) ? 'fas' : 'far'"
                        >      
                        </i>  
                    </li> 
                </div>
            
                  <div class="overview">
                        <div :class="{'visible': index === activeFilm }" class="cast">              
                          <p v-for="(cast, i) in arrayCast" :key="i"> {{cast.name}}  </p>               
                        </div>  
                    
                      <div :class="{'invisible': index === activeFilm} " class="container-show-more">
                        <li> <strong>Trama:</strong>  {{item.overview}} </li> 

                        <p @click="showMore(index)"> 
                          Show more
                        </p>
                      </div>  
                  </div>
                    
                </ul>
            </div>
         </div>
      </div>
  </vue-custom-scrollbar>    
    </div>

    <div  v-if="!searchClicked"  class="global-card">
     <vue-custom-scrollbar class="scroll-area"  :settings="settings" @ps-scroll-y="scrollHanle">  
     <div class="title-genr fc-flex fc-align-center"> <h2> RACCOMANDATI PER TE </h2> </div>
      
      <div class="container-card fc-flex">

        <!-- <p> {{this.filteredCards[activeFilm].id}} </p> -->
        <div v-for="(item, index) in arrayRecommended" :key="item.id" class="card">
            <div class="card-img">

              <img v-if="item.poster_path !== null " :src="'http://image.tmdb.org/t/p/w300' + item.poster_path" alt="">
              <div v-else class="card fc-flex fc-align-center fc-justify-center">
                <h2 v-if="item.hasOwnProperty('title')"> {{item.title}} </h2>
                <h2 v-if="item.hasOwnProperty('name')"> {{item.name}} </h2>
              </div>
            </div>

            <div class="card-text">
              <div class="container-title">
                <h2 v-if="item.hasOwnProperty('title')"> {{item.title}} </h2>
                <h2 v-if="item.hasOwnProperty('name')"> {{item.name}} </h2>
              </div>
      
              <ul>
                <div class="content-card-top">
                    <li v-if="item.hasOwnProperty('original_title')"> Titolo originale: {{item.original_title}} </li>
                    <li v-if="item.hasOwnProperty('original_name')"> Titolo originale: {{item.original_name}} </li>
                    <li>
                        Lingua: 
                        <img 
                          class="language" 
                          v-if="langFunction(item) !== ''" :src="langFunction(item)" :alt="item.original_language"
                        >
                        <span v-else>{{ item.original_language }}</span>

                    </li>
                    <li> 
                        <i v-for="(star, index) in 5" :key="index" class="fa-star"  
                          :class="index < Math.round(item.vote_average / 2 ) ? 'fas' : 'far'"
                        >      
                        </i>  
                    </li> 
                </div>
            
                  <div class="overview">
                        <div :class="{'visible': index === activeFilm }" class="cast">              
                          <p v-for="(cast, i) in arrayCast" :key="i"> {{cast.name}}  </p>               
                        </div>  
                    
                      <div :class="{'invisible': index === activeFilm} " class="container-show-more">
                        <li> <strong>Trama:</strong>  {{item.overview}} </li> 

                        <p @click="showMore(index)"> 
                          Show more
                        </p>
                      </div>  
                  </div>
                    
                </ul>
            </div>
        </div>
      </div>
     </vue-custom-scrollbar> 
    </div>

    <div  v-if="!searchClicked"  class="global-card">
     <vue-custom-scrollbar class="scroll-area"  :settings="settings" @ps-scroll-y="scrollHanle">  
      <div class="title-genr fc-flex fc-align-center"> <h2> FILM PIU' VOTATI </h2> </div>
      
      <div class="container-card fc-flex">

        <!-- <p> {{this.filteredCards[activeFilm].id}} </p> -->
        <div v-for="(item, index) in arrayTop" :key="item.id" class="card">
            <div class="card-img">

              <img v-if="item.poster_path !== null " :src="'http://image.tmdb.org/t/p/w300' + item.poster_path" alt="">
              <div v-else class="card fc-flex fc-align-center fc-justify-center">
                <h2 v-if="item.hasOwnProperty('title')"> {{item.title}} </h2>
                <h2 v-if="item.hasOwnProperty('name')"> {{item.name}} </h2>
              </div>
            </div>

            <div class="card-text">
              <div class="container-title">
                <h2 v-if="item.hasOwnProperty('title')"> {{item.title}} </h2>
                <h2 v-if="item.hasOwnProperty('name')"> {{item.name}} </h2>
              </div>
      
              <ul>
                <div class="content-card-top">
                    <li v-if="item.hasOwnProperty('original_title')"> Titolo originale: {{item.original_title}} </li>
                    <li v-if="item.hasOwnProperty('original_name')"> Titolo originale: {{item.original_name}} </li>
                    <li>
                        Lingua: 
                        <img 
                          class="language" 
                          v-if="langFunction(item) !== ''" :src="langFunction(item)" :alt="item.original_language"
                        >
                        <span v-else>{{ item.original_language }}</span>

                    </li>
                    <li> 
                        <i v-for="(star, index) in 5" :key="index" class="fa-star"  
                          :class="index < Math.round(item.vote_average / 2 ) ? 'fas' : 'far'"
                        >      
                        </i>  
                    </li> 
                </div>
            
                  <div class="overview">
                        <div :class="{'visible': index === activeFilm }" class="cast">              
                          <p v-for="(cast, i) in arrayCast" :key="i"> {{cast.name}}  </p>               
                        </div>  
                    
                      <div :class="{'invisible': index === activeFilm} " class="container-show-more">
                        <li> <strong>Trama:</strong>  {{item.overview}} </li> 

                        <p @click="showMore(index)"> 
                          Show more
                        </p>
                      </div>  
                  </div>
                    
                </ul>
            </div>
        </div>
    </div>
  </vue-custom-scrollbar> 
    </div>

    <div  v-if="!searchClicked"  class="global-card">
      <vue-custom-scrollbar class="scroll-area"  :settings="settings" @ps-scroll-y="scrollHanle">  
       <div class="title-genr fc-flex fc-align-center"> <h2> SERIE TV POPOLARI </h2> </div>
      
        <div class="container-card fc-flex">

        <!-- <p> {{this.filteredCards[activeFilm].id}} </p> -->
         <div v-for="(item, index) in arrayTvPop" :key="item.id" class="card">
            <div class="card-img">

              <img v-if="item.poster_path !== null " :src="'http://image.tmdb.org/t/p/w300' + item.poster_path" alt="">
              <div v-else class="card fc-flex fc-align-center fc-justify-center">
                <h2 v-if="item.hasOwnProperty('title')"> {{item.title}} </h2>
                <h2 v-if="item.hasOwnProperty('name')"> {{item.name}} </h2>
              </div>
            </div>

            <div class="card-text">
              <div class="container-title">
                <h2 v-if="item.hasOwnProperty('title')"> {{item.title}} </h2>
                <h2 v-if="item.hasOwnProperty('name')"> {{item.name}} </h2>
              </div>
      
              <ul>
                <div class="content-card-top">
                    <li v-if="item.hasOwnProperty('original_title')"> Titolo originale: {{item.original_title}} </li>
                    <li v-if="item.hasOwnProperty('original_name')"> Titolo originale: {{item.original_name}} </li>
                    <li>
                        Lingua: 
                        <img 
                          class="language" 
                          v-if="langFunction(item) !== ''" :src="langFunction(item)" :alt="item.original_language"
                        >
                        <span v-else>{{ item.original_language }}</span>

                    </li>
                    <li> 
                        <i v-for="(star, index) in 5" :key="index" class="fa-star"  
                          :class="index < Math.round(item.vote_average / 2 ) ? 'fas' : 'far'"
                        >      
                        </i>  
                    </li> 
                </div>
            
                  <div class="overview">
                        <div :class="{'visible': index === activeFilm }" class="cast">              
                          <p v-for="(cast, i) in arrayCast" :key="i"> {{cast.name}}  </p>               
                        </div>  
                    
                      <div :class="{'invisible': index === activeFilm} " class="container-show-more">
                        <li> <strong>Trama:</strong>  {{item.overview}} </li> 

                        <p @click="showMore(index)"> 
                          Show more
                        </p>
                      </div>  
                  </div>
                    
                </ul>
            </div>
        </div>
     </div>
   </vue-custom-scrollbar> 
    </div>

    <div  v-if="searchClicked"  class="global-card">
      <vue-custom-scrollbar class="scroll-area"  :settings="settings" @ps-scroll-y="scrollHanle"> 
       <div class="title-genr fc-flex fc-align-center"> <h2>FILM </h2> </div>
      
        <div class="container-card fc-flex">

        <!-- <p> {{this.filteredCards[activeFilm].id}} </p> -->
         <div v-for="(item, index) in arrayMovie" :key="item.id" class="card">
            <div class="card-img">

              <img v-if="item.poster_path !== null " :src="'http://image.tmdb.org/t/p/w300' + item.poster_path" alt="">
              <div v-else class="card fc-flex fc-align-center fc-justify-center">
                <h2 v-if="item.hasOwnProperty('title')"> {{item.title}} </h2>
                <h2 v-if="item.hasOwnProperty('name')"> {{item.name}} </h2>
              </div>
            </div>

            <div class="card-text">
              <div class="container-title">
                <h2 v-if="item.hasOwnProperty('title')"> {{item.title}} </h2>
                <h2 v-if="item.hasOwnProperty('name')"> {{item.name}} </h2>
              </div>
      
              <ul>
                <div class="content-card-top">
                    <li v-if="item.hasOwnProperty('original_title')"> Titolo originale: {{item.original_title}} </li>
                    <li v-if="item.hasOwnProperty('original_name')"> Titolo originale: {{item.original_name}} </li>
                    <li>
                        Lingua: 
                        <img 
                          class="language" 
                          v-if="langFunction(item) !== ''" :src="langFunction(item)" :alt="item.original_language"
                        >
                        <span v-else>{{ item.original_language }}</span>

                    </li>
                    <li> 
                        <i v-for="(star, index) in 5" :key="index" class="fa-star"  
                          :class="index < Math.round(item.vote_average / 2 ) ? 'fas' : 'far'"
                        >      
                        </i>  
                    </li> 
                </div>

                  <div class="overview">
                        <div :class="{'visible': index === activeFilm }" class="cast">              
                          <p v-for="(cast, i) in arrayCast" :key="i"> {{cast.name}}  </p>               
                        </div>  
                    
                      <div :class="{'invisible': index === activeFilm} " class="container-show-more">
                        <li> <strong>Trama:</strong>  {{item.overview}} </li> 

                        <p @click="showMore(index)"> 
                          Show more
                        </p>
                      </div>  
                  </div>
    
                </ul>
            </div>
        </div>
      </div>
     </vue-custom-scrollbar> 

   </div>

    <div  v-if="searchClicked"  class="global-card">
     <vue-custom-scrollbar class="scroll-area"  :settings="settings" @ps-scroll-y="scrollHanle"> 
      <div class="title-genr fc-flex fc-align-center"> <h2> SERIE TV </h2> </div>
      
       <div class="container-card fc-flex">
      
        <!-- <p> {{this.filteredCards[activeFilm].id}} </p> -->
         <div v-for="(item, index) in arrayTv" :key="item.id" class="card">
             <div class="card-img">

              <img v-if="item.poster_path !== null " :src="'http://image.tmdb.org/t/p/w300' + item.poster_path" alt="">
              <div v-else class="card fc-flex fc-align-center fc-justify-center">
                <h2 v-if="item.hasOwnProperty('title')"> {{item.title}} </h2>
                <h2 v-if="item.hasOwnProperty('name')"> {{item.name}} </h2>
              </div>
            </div>

            <div class="card-text">
              <div class="container-title">
                <h2 v-if="item.hasOwnProperty('title')"> {{item.title}} </h2>
                <h2 v-if="item.hasOwnProperty('name')"> {{item.name}} </h2>
              </div>
      
              <ul>
                <div class="content-card-top">
                    <li v-if="item.hasOwnProperty('original_title')"> Titolo originale: {{item.original_title}} </li>
                    <li v-if="item.hasOwnProperty('original_name')"> Titolo originale: {{item.original_name}} </li>
                    <li>
                        Lingua: 
                        <img 
                          class="language" 
                          v-if="langFunction(item) !== ''" :src="langFunction(item)" :alt="item.original_language"
                        >
                        <span v-else>{{ item.original_language }}</span>

                    </li>
                    <li> 
                        <i v-for="(star, index) in 5" :key="index" class="fa-star"  
                          :class="index < Math.round(item.vote_average / 2 ) ? 'fas' : 'far'"
                        >      
                        </i>  
                    </li> 
                </div>
            
                  <div class="overview">
                        <div :class="{'visible': index === activeFilm }" class="cast">              
                          <p v-for="(cast, i) in arrayCast" :key="i"> {{cast.name}}  </p>               
                        </div>  
                    
                      <div :class="{'invisible': index === activeFilm} " class="container-show-more">
                        <li> <strong>Trama:</strong>  {{item.overview}} </li> 

                        <p @click="showMore(index)"> 
                          Show more
                        </p>
                      </div>  
                  </div>
                    
                </ul>
            </div>
          </div>
        </div>
      </vue-custom-scrollbar> 
    </div>


  </main>
</template>

<script>


import axios from 'axios'
import vueCustomScrollbar from 'vue-custom-scrollbar'
import "vue-custom-scrollbar/dist/vueScrollbar.css"

export default {
  name: 'Main',
  props:{
     arrayConcat: Array,
     arrayTrend: Array,
     arrayMovie: Array,
     arrayTv: Array,
     arrayRecommended: Array,
     arrayTop: Array,
     arrayTvPop: Array,
     searchClicked: Boolean
     
  },

  components: {
    vueCustomScrollbar
  },

     data() {
      return {
         imgURL: 'https://image.tmdb.org/t/p/w342/',
         selected: '',
         activeFilm: '',
         apiKey:'api_key=2773f939423c2a6dac0e7e805c296cf6&',
         apiMovieGeneral:'https://api.themoviedb.org/3/movie/',
         arrayCast: [],

        settings: {
          suppressScrollY: false,
          suppressScrollX: false,
          // wheelPropagation: false,
          // useBothWheelAxed: true
       }
      }
   },

  //   computed:{

  //   filteredCards(){
    
  //     if(this.selected == 0 || this.selected == '' ){
  //       return this.arrayConcat;

  //     }else if(this.selected == 1){
  //       return this.arrayConcat.filter( item => {
  //       return Object.prototype.hasOwnProperty.call(item, 'title')
  //     })
  //     }
  //       return this.arrayConcat.filter( item => {
  //       return Object.prototype.hasOwnProperty.call(item, 'name')
  //     })
      

  //   }

  // },
    
  
  methods:{

    scrollHanle(evt) {
      console.log(evt)
    },

       langFunction(item) {
         const lang = item.original_language;
         let imgUrl = '';
         if (lang.toLowerCase().includes('en')) return imgUrl = require('../assets/img/en.png');
         if (lang.toLowerCase().includes('it')) return imgUrl = require('../assets/img/it.png');
         
         
         return imgUrl;
      },

      switchSelect(event) {
      this.selected = event.target.value;
    },

    showMore(index){

      // this.castVisible = true;
       this.activeFilm = index
      // console.log('ho clickato', this.castVisible);
      // console.log('ho clickato e basta');
       axios.get(`${this.apiMovieGeneral}${this.filteredCards[this.activeFilm].id}'/credits?'${this.apiKey}`)
      .then( r => {
        this.arrayCast = r.data.cast
      })
      .catch( e => {
        console.log(e);
      })

    },


  }
}

</script>

<style lang="scss">

.scroll-area {
  position: relative;
}

//  ::-webkit-scrollbar-track{
//       box-shadow: inset 0 0 5px grey; 
//       border-radius: 10px;
//   }

//   ::-webkit-scrollbar-thumb {
//      background: red; 
//      border-radius: 10px;
//   }

//   ::-webkit-scrollbar-thumb:hover {
//      background: #b30000; 
//    }
  

 main{
  position: relative;
  min-height: 100vh;
  padding-top: 100px;
   
  .container-card{
    position: relative;
    width: 100%;
    // overflow-x: auto;
     
  }
 

  
  
   .card{
     position: relative;
     color: white;
     height: 410px;
     width: 300px;
     margin: 15px;
     padding: 10px;
     flex-shrink: 0;
      .content-card-top{
        height: 35%;
      }
      .container-title{
        height: 50px;
        overflow: hidden;
      }
       h2{
        font-size: 2vh;
         
       }
       ul{
         position: relative;
         height: 330px;
       }
       li{
         padding-bottom: 10px;
       }
       .fas{
         color:yellow;
       }
       .far{
         color:gray;
       }

   }

.global-title{
        height: 60px;
        width: 100%;
        color: white;
      }
    select{
      margin-left: 30px;
      width: 120px;
      height: 22px;
      border: none;
      border-radius: 5px;
    }

    .title-genr{
      // background-color: rgb(49, 10, 10);
      height: 50px;
      color: white;
      border-top: 1px solid rgb(92, 87, 87);
       h2{
         margin-left: 15px;
       }
    }

 }

 .overview{
   position: relative;
   font-size: 14px;
   width: 100%;
   height: 60%;
   overflow: auto;
    p{
      position: absolute;
      cursor: pointer;
      color: red;
    }
 }

 .cast{
   position: absolute;
   width: 100%;
   display: none;
 }

 .visible{
   display: block;
 }

 .invisible{
   display: none;
 }

  .language {
    width: 23px;
   }

.card-text{
  opacity: 0;
  transition: all 2s;
  z-index: 999;
}
.card-img{ 
  opacity: 1;
  transition: all 2s;
   img{
         max-height: 100%;
         width: 100%;
       }
}
.card:hover .card-text{
  opacity: 1;
}
.card:hover .card-img{
  opacity: 0;
}

.card-img{
  position: absolute;
  left: 0;
  top: 0;
  height: 410px;
  width: 300px;
}

</style>