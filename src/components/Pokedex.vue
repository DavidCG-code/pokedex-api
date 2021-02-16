<template>

  <PokemonSearch
  :API_URL = "API_URL"
  @setPokemonUrl="setPokemonUrl" />

  <PokemonList 
  :imageUrl = "imageUrl" 
  :API_URL = "API_URL"
  @setPokemonUrl="setPokemonUrl"/>

  <Pokemon
  v-if="showDetail"
  :pokemon = "pokemon"
  @click = "close"/>

</template>

<script>
import { ref, reactive} from 'vue';
import PokemonSearch from './PokemonSearch.vue'
import PokemonList from './PokemonList.vue';
import Pokemon from './Pokemon.vue';

export default {
 
  components: {
    PokemonList,
    Pokemon,
    PokemonSearch
  },
  setup(){
    const imageUrl = ref('');
    const image = ref('');
    const API_URL = ref('');
    const showDetail = ref(false);


    API_URL.value = 'https://pokeapi.co/api/v2/pokemon/';
    imageUrl.value ="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/";

  
      const pokemon = reactive({
        data: '',
        image: imageUrl.value
      })

  function setPokemonUrl(url){
    pokemon.data = url;
    showDetail.value = true
  }


  function close(){
    pokemon.data = ''
    showDetail.value = false
  }



    return{
      setPokemonUrl,
      pokemon,
      imageUrl,
      API_URL,
      showDetail,
      close,
      image,
  
     
     
    }

  }
 
}
</script>

