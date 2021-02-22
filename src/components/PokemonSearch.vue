<template>
  <div class="col-12 ">
    <form @submit.prevent="setPokemonUrl">
      <input type="text" v-model="search" class="input-search" placeholder="Search a Pokemon..." >
      <figure class="button-search">
        <img src="../assets/loupe.svg" width="20" height="20" alt="">
      </figure>
    </form>
     
  </div>
</template>


<script>
import { ref } from 'vue';
export default {
  props:[
    'API_URL',
   
  ],
  setup(props, context){
    const search = ref('');

    function setPokemonUrl(){
      if(search.value !== ''){
        context.emit('setPokemonUrl', props.API_URL + search.value);
        
        search.value = '';
      }
    
    }
 console.log(props.API_URL);
    return{
      search,
      setPokemonUrl
    }
  }

}
</script>

<style lang="scss">
form{
 position:relative;
  .input-search{
    border: none;
    padding: 8px 0;
    width: 100%;
    border-bottom: 2px solid black;
    background: none;
    font-size: 1.2rem;
    &:focus, &:active{
      outline: none;
    }
  }
  .button-search{
    position: absolute;
    bottom: 5px;
    right: 5px;
  }
}

</style>