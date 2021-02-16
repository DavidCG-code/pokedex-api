<template  >
 <div class="container">
  <div class="pokeCard">
    <div class="pokeCard__image">
      <figure>
        <img :src="pokemon.image+poke.id+'.png'" :alt="poke.name" >
      </figure>
    </div>

    <div class="pokeCard__name">
      <div class="pokeCard__name--order">
        <figure>
          <img src="../assets/pokebola.svg" width="19" height="19" alt="">
        </figure>
        <p> {{poke.id}}</p>
      </div>
      <div class="pokeCard__name--text">
         <p>{{poke.name}}</p>
      </div>
    </div>

    <div class="pokeCard__types">
      <p v-for="type in types" :key="type.id" :class="type.color">
        {{type.name}}
      </p>
    </div>

    <div class="pokeCard__physicDates">
      <p>Height: {{poke.height / 10}} m</p>
      <p>Weight: {{poke.weight / 10}} Kg</p>
    </div>

    <hr>

    <div class="pokeCard__stats" >
      <div class="pokeCard__stats--title">
        <h4>Stats:</h4>
      </div>
      <div class="pokeCard__stats--values">
        <p v-for="stat in stats" :key="stat.id">
          {{stat.name}}: <span>{{stat.value}}</span>
        </p>
      </div>
    </div>

    <hr>

    <div class="pokeCard__abilities">
      <div class="pokeCard__abilities--title">
        <h4>Abilities:</h4>
      </div>
      <div class="pokeCard__abilities--ability">
        <p v-for="ability in abilities" :key="ability.id">
          {{ability.name}}
        </p>
      </div>
    </div>

    <hr>

    <div class="pokeCard__description">

    </div>
  </div>
 </div>
 
</template>


<script>
import {ref} from 'vue';
export default {
  props: [
    'pokemon',
   
    
  ],
  setup(props) {
    const show = ref(false);
    const poke = ref('');
    const types = ref([]);
    const stats = ref([]);
    const abilities = ref([]);

    async function fetchData(){
      const response = await fetch(props.pokemon.data);
      const json = await response.json();
    
      show.value = true;
      poke.value = json;

      poke.value.types.map((x)=>{
        types.value.push({
          name: x.type.name,
          color: x.type.name
        });
      });

      poke.value.stats.map((x)=>{
        stats.value.push({
          name: x.stat.name,
          value: x.base_stat
        })
      });

      poke.value.abilities.map((x)=>{
        abilities.value.push({
          name: x.ability.name
        });
      });


      console.log(poke.value);

      
    }

    return{
      fetchData,
      poke,
      show,
      types,
      stats,
      abilities
      
    }
   
  },
  created(){
    this.fetchData();

  }

}
</script>



<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Josefin+Sans:wght@700&family=Quicksand:wght@300;400&display=swap');
  hr{
    margin: 1rem auto;
    width: 90%;
  }
  .container{
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;
    background-color: rgba(12, 12, 12, 0.452);
    z-index: 1;

    .pokeCard{
       display: flex;
       flex-direction: column;
      width: 85%;
      height: 65%;
      margin: 6rem auto 0;
      background-color: #f5f5f5;
      border-radius: 20px;
      position: relative;

      @media(min-width: 768px) {
        height: 55%;
      }
        @media(min-width: 1024px){
          width: 35%;
        }

      &__image{
        background-color: rgb(190, 190, 190);
        width: 100px;
        height: 100px;
        border-radius: 50%;
        
        position: absolute;
        top: -3rem;
        left: 35%;
        text-align: center;

        @media(min-width: 768px){
          left: calc(100% / 2.5);
          width: 120px;
          height: 120px;
          img{
            width: 100%;
          }
        }
        @media(min-width: 1024px){
          left: calc(100% / 2.5);
        }
        
      }

      &__name{
        padding-top: 4rem;
        margin: 0 auto;
        font-size: 1.2rem;
        
        @media(min-width: 768px) {
          padding-top: 6rem;
        }
        &--order{
          
          display: flex;
          align-items: center;
          justify-content: center;
          figure{
            margin-right: 0.75rem;
          }
        }

        &--text{
          text-transform: capitalize;
       
          
          
        }
      }

      &__types{
        margin: 0 auto;
        text-transform: capitalize;
        font-size: 0.85rem;
        margin-top: 0.50rem;
        display: flex;
        p{
          border-radius: 20px;
          padding: 0.25rem 0.75rem 0.15rem;
          color: #f5f5f5;
          
        }
        p:not(:last-of-type){
          margin-right: 0.5rem;
        }
      }

      &__physicDates{
        display: flex;
        font-size: 0.80rem;
        margin: 0.5rem auto 0;
        p:not(:last-of-type){
          margin-right: 0.75rem;
        }
      }

      &__stats{
        display: flex;
        flex-direction: column;
        padding: 0 1rem;
        &--title{
          padding: 0.25rem 0.50rem;
        }
        &--values{
          display: flex;
          flex-wrap: wrap;
          
         p{
          flex-basis: 50%;
          font-size: 0.75rem;
          display: flex;
          justify-content: space-between;
          text-transform: capitalize;
          padding: 0 0.50rem;
         }
        }
        
      }

      &__abilities{
        display: flex;
        flex-direction: column;
        padding: 0 1rem;
        &--title{
          padding: 0.25rem 0.50rem;
        }
        &--ability{
          padding-top: 0.50rem;
          display: flex;
          align-items: center;
         
          p{
            flex-basis: 33%;
            text-align: center;
            border-radius: 20px;
            padding: 0.25rem 0.30rem;
            font-size: 0.75rem;
            background-color:#d45454;
            box-shadow: 0px 3px 6px #d4545488;
            color: #f5f5f5;
          }
          p:not(:last-of-type){
            margin-right: 1rem;
          }
        }
      }
     
    }
  //Type Colors
    .grass{
      background-color: rgb(92, 194, 92);
      box-shadow: 0px 3px 3px rgba(92, 194, 92, 0.500);
    }
    .poison{
      background-color: rgb(187, 70, 187);
      box-shadow: 0px 3px 3px rgba(187, 70, 187, 0.500);
    }
    .fire{
      background-color: rgb(228, 117, 66);
      box-shadow: 0px 3px 3px rgba(228, 117, 66, 0.500);
    }
    .water{
      background-color: rgb(60, 127, 216);
      box-shadow: 0px 3px 3px rgba(60, 127, 216, 0.500);
      
    }
    .flying{
      background-color: rgb(106, 144, 224);
      box-shadow: 0px 3px 3px rgba(106, 144, 224, 0.500);
    }
    .bug{
      background-color: rgb(115, 179, 55);
      box-shadow: 0px 3px 3px rgba(115, 179, 55, 0.500);
    }
    .normal{
      background-color: rgb(204, 175, 131);
      box-shadow: 0px 3px 3px rgba(204, 175, 131, 0.500);
    }
    .electric{
      background-color: rgb(230, 204, 93);
      box-shadow: 0px 3px 3px rgba(230, 204, 93, 0.500);
    }
    .ground{
      background-color: rgb(185, 149, 94);
      box-shadow: 0px 3px 3px rgba(185, 149, 94, 0.500);
    }
    .fairy{
      background-color: rgb(221, 131, 217);
      box-shadow: 0px 3px 3px rgba(221, 131, 217, 0.500);
    }
    .fighting{
      background-color: rgb(201, 87, 67);
      box-shadow: 0px 3px 3px rgba(201, 87, 67, 0.500);
    }
    .psychic{
      background-color: rgb(211, 123, 211);
      box-shadow: 0px 3px 3px rgba(211, 123, 211, 0.500);
    }
    .rock{
      background-color: rgb(163, 138, 108);
      box-shadow: 0px 3px 3px rgba(163, 138, 108, 0.500);
    }
    .ghost{
      background-color: rgb(139, 109, 177);
      box-shadow: 0px 3px 3px rgba(139, 109, 177, 0.500);
    }
    .steel{
      background-color: rgb(163, 163, 163);
      box-shadow: 0px 3px 3px rgba(163, 163, 163, 0.500);
    }
    .ice{
      background-color: rgb(112, 198, 255);
      box-shadow: 0px 3px 3px rgba(112, 198, 255, 0.500);
    }
    .dragon{
      background-color: rgb(111, 77, 206);
      box-shadow: 0px 3px 3px rgba(111, 77, 206, 0.500);
    }
    .dark{
      background-color: rgb(85, 85, 85);
      box-shadow: 0px 3px 3px rgba(85, 85, 85, 0.500);
    }
    
  }
</style>