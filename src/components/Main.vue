<template>
<main>
  <div class="global-title fc-container">
   <select @change="switchSelect($event)">
     <option selected value="0">Tutto</option>
     <option value="1">Film</option>
     <option value="2">Serie Tv</option>
   </select>
  </div>
  <div class="fc-container fc-flex fc-wrap">
    <div v-for="item in filteredCards" :key="item.id" class="card">
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
                <li> <strong>Trama:</strong>  {{item.overview}} </li> 
              </div>  
         
            </ul>
         </div>
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
         selected: '',
      }
   },


    computed:{

    filteredCards(){
    
      if(this.selected == 0 || this.selected == '' ){
        console.log('>>>>>>>>>>>>>>>>>>>',this.selected);
        return this.arrayConcat;

      }else if(this.selected == 1){
        return this.arrayConcat.filter( item => {
        return Object.prototype.hasOwnProperty.call(item, 'title')
      })
      }
        return this.arrayConcat.filter( item => {
        return Object.prototype.hasOwnProperty.call(item, 'name')
      })
      


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

      switchSelect(event) {
      this.selected = event.target.value;
    }

  }
}

</script>

<style lang="scss">

 main{
  min-height: calc(100vh - 100px);
   .card{
     position: relative;
     color: white;
     height: 410px;

     width: 300px;
     margin: 18px;
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

.card-text{
  opacity: 0;
  transition: all 2s;
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