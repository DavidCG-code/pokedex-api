<template>
  <div class="title">
    <h1>Pokedex</h1>
  </div>
  <div class="container">
    <Pokedex/>
  </div>
  
</template>

<script>
import Pokedex from './components/Pokedex.vue'

export default {
  name: 'App',
  components: {
    Pokedex
  },

}
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Josefin+Sans:wght@700&family=Quicksand:wght@300;400&display=swap');
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;

}
body{
 background-color: #d45454;
}


#app {
  font-family: 'Josefin Sans';
  color: #212121
}

.title{
  padding: 2rem 0;
  text-align: center;
}


</style>
