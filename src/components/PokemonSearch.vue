<template>
  <div class="input-search">
    <form @submit.prevent="setPokemonUrl">
      <input type="text" v-model="search" placeholder="Search a Pokemon..." >
     
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

<style lang="scss" scoped>
  .input-search{
    display: flex;
    justify-content: center;
    margin-bottom: 1.2rem;
 

    button{
      padding: 0 8px;
      border: none;
      margin-left: 1rem;
    }
  }
</style>