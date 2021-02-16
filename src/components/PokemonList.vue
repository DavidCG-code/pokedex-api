<template>
    <div class="pokemons"
    v-for="(poke,index) in pokemons" :key="'poke'+index.id"
    @click="setPokemonUrl(poke.url)" >
      <div class="pokemons__number">
        <figure class="pokemons__number--image">
          <img src="../assets/pokebola.svg" width="18" height="18" alt="">
        </figure>
        <p class="pokemons__number--text">
          {{poke.id}}
        </p>
      </div>
      <div class="pokemons__box">
        <img :src="imageUrl + poke.id + '.png'" width="85" height="85" alt="">
        <p>{{poke.name}}</p>
      </div>
    </div>

  <div class="arrows">
    <button type="button" @click="previous" class="arrows__inverse"><img src="../assets/flecha-correcta.svg" alt="" width="40" height="40"></button>
    <button type="button" @click="next" ><img src="../assets/flecha-correcta.svg" alt="" width="40" height="40"></button>
  </div>

</template>

<script>
import {ref} from 'vue';

export default {

  props: [
    'imageUrl',
    'API_URL',
    
  ],
  emits: ["setPokemonUrl"],
  setup(props, context) {

    const pokemons = ref([]);
    const nextUrl = ref('');
    const previousUrl = ref('');



    //General function Pokemon list
    async function getPokemons(currentUrl){
      const response = await fetch(currentUrl);
      const json = await response.json();

      json.results.forEach(pokemon => {
        
        pokemon.id = pokemon.url.split('/').filter(function(part){
          return !!part
        }).pop();
        
      });
      pokemons.value = json.results;
      nextUrl.value = json.next;
      previousUrl.value = json.previous;

      
    }

    getPokemons(props.API_URL);
      
  
    //Next and Previous

    function next(){
      getPokemons(nextUrl.value)
    }

      function previous(){
      getPokemons(previousUrl.value)
    }


    //Info Pokemon

    function setPokemonUrl(url){
      context.emit('setPokemonUrl', url)
    }
  

    //Get only one Pokemon

    return {
      pokemons,
       setPokemonUrl,
      next,
      previous
    }
 }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" >
 .pokemons{
   width: 50%;
   margin: 0 auto;
   background-color: #f5f5f5;
   margin-bottom: 1rem;
   border-radius: 20px;
   overflow: hidden;
   box-shadow: 0px 3px 6px #74747486;
   &__number{
     padding: 0.75rem 1rem 0.5rem;
     background-color: #74747486;
     display: flex;
     align-items: center;
    &--image{
      margin-right: 0.5rem;
    }
    &--text{
      font-size: 1rem;
    }
     
   }
   &__box{
    text-align: center;
     
    img{
      width: 100px;
      height: 100px;
    }
    p{
      margin-bottom: 1rem;
      text-transform: capitalize;
    }
   }
 }



 .arrows{
   
   position: fixed;
   bottom: 50px;
   width: 100%;
   display: flex;
   justify-content: space-between;
   
   

   &__inverse{
     transform: rotate(180deg);
     margin-left: 1rem;
   }

   button{
     margin-right: 1rem;
     background: none;
     border: none;
    cursor: pointer;
    &:focus,&:active{
      outline: none;
    }
   }

   @media(min-width: 1024px){
    &__inverse{
      margin-left: 5rem;
    }

    button{
      margin-right: 5rem;
    }
   }
 }
</style>