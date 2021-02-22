<template>
    <div class="pokemons col-6 col-md-3"
    v-for="(poke,index) in pokemons" :key="'poke'+index.id"
    @click="setPokemonUrl(poke.url)" >

      <div class="pokemons__box">
        <div class="pokemons__box__number d-flex align-items-center p-2">
          <figure class="pokemons__box__number--image">
            <img src="../assets/pokebola.svg" width="18" height="18" alt="">
          </figure>
          <p class="pokemons__box__number--text">
            {{poke.id}}
          </p>
        </div>
        <div class="pokemons__box__image p-2">
          <figure>
            <img :src="imageUrl + poke.id + '.png'" width="85" height="85" alt="">
          </figure>
          <p>{{poke.name}}</p>
        </div>
      </div>
    </div>

  <div class="arrows">
    <button type="button" @click="previous" ><img src="../assets/flecha-correcta.svg" class="arrows__inverse" alt="" width="40" height="40">Prev</button>
    <button type="button" @click="next" >Next<img src="../assets/flecha-correcta.svg" alt="" width="40" height="40"></button>
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
   &:nth-of-type(19),&:nth-of-type(20){
     margin-bottom: 5rem;
   }
   &__box{
    text-align: center;
    background-color: #f5f5f5;
    border-radius: 20px;
    overflow: hidden;
    box-shadow: 0px 3px 6px #74747486;
    &__number{
     
     background-color: #74747486;
      &--image{
        margin-right: 0.5rem;
        height: 18px;
      }
      &--text{
        font-size: 1rem;
      }
    }

    &__image{
      figure{
        width: 100%;

        img{
          width:100px;
          height:100px;
        }
      }
      p{
        text-transform: capitalize;
      }
    }

   }
 }



 .arrows{
   padding: 1rem;
   position: fixed;
   bottom: 0;
   width: 100%;
   display: flex;
   justify-content: space-between;
   background-color: #74747486;
   

   &__inverse{
     transform: rotate(180deg);
   }

   button{
     margin-right: 1rem;
     background: none;
     border: none;
     display: flex;
     align-items: center;
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