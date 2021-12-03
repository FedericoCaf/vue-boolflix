<template>
  <header class="fc-flex fc-between fc-align-center">
    <div class="logo fc-flex fc-align-center fc-justify-center"> BOOLFLIX </div>

    <div class="search-bar fc-flex fc-between fc-align-center">
      <input 
        v-model="querySearch" 
        placeholder="cerca film o serie tv"
        @keyup.enter="$emit('sendQuerySearch', querySearch)"
      >
      <button @click="$emit('sendQuerySearch', querySearch)" > CERCA </button>   
    </div>  
  </header>
</template>

<script>

export default {
  name: 'Header',

  data(){
    return{
      querySearch: '',
    }
  }
}
</script>

<style lang="scss" scoped>


 header{
   height: 100px;
  //  background-color: black;
   background: linear-gradient(rgb(14, 0, 0), black);
   color: white;
    .logo{
      width: 200px;
      height: 80px;
      font-size: 35px;
      color:rgb(199, 15, 15);
    }
    .search-bar{
      width: 300px;
      height: 80px;
      padding: 10px;
        input{
         width: 65%;
         height: 25px;
         border: none;
         padding-left: 5px;
         border-radius: 5px;;
        }
        button{
          width: 30%;
          height: 25px;
          border-radius: 0;
          border: none;
          cursor: pointer;
          background-color: rgb(139, 16, 16);
          color: white;
          font-weight: bold;
          border-radius: 5px;
        }
    }
 }

</style>