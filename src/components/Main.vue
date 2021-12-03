<template>
  <main class="fc-container fc-flex fc-wrap">
    <div v-for="item in arrayConcat" :key="item.id" class="card">
      <div class="card-img">
        <img :src="'http://image.tmdb.org/t/p/w300' + item.poster_path" alt="">
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
                <li> <strong>Trama:</strong>  {{item.overview}} </li> 
              </div>  
         
          </ul>
      </div>

        
    </div>

  </main>
</template>

<script>


export default {
  name: 'Main',
  props:{
     arrayConcat: Array
  },

     data() {
      return {
         imgURL: 'https://image.tmdb.org/t/p/w342/',
      }
   },
  
  methods:{
       langFunction(item) {
         const lang = item.original_language;
         let imgUrl = '';
         if (lang.toLowerCase().includes('en')) return imgUrl = require('../assets/img/en.png');
         if (lang.toLowerCase().includes('it')) return imgUrl = require('../assets/img/it.png');
         
         
         return imgUrl;
      },
  },

}
</script>

<style lang="scss">

 main{
  min-height: calc(100vh - 100px);
  overflow: hidden;
   .card{
     position: relative;
     color: white;
     height: 410px;
     width: 300px;
    //  border: 1px solid white;
     margin: 25px;
     padding: 10px;
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

      //  img{
      //    height: 100%;
      //  }
   }

 }

 .overview{
   font-size: 14px;
   width: 100%;
   height: 60%;
   overflow: auto;
 }

  .language {
        width: 23px;
   }

   ::-webkit-scrollbar {
    display: none;
}

//    ::-webkit-scrollbar {
//   width: 10px;
// }
// ::-webkit-scrollbar-track {
//   background: #f1f1f1; 
// }
// ::-webkit-scrollbar-thumb {
//   background: rgb(201, 191, 191); 
// }
// ::-webkit-scrollbar-thumb:hover {
//   background: rgb(167, 162, 162); 
// }

.card-text{
  opacity: 0;
  transition: all 2s;
}
.card-img{
  opacity: 1;
  transition: all 2s;
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