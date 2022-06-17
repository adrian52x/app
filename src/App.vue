<template>
  
  <PokemonCard />

</template>

<script>
import PokemonCard from './components/PokemonCard.vue'

export default {
  name: 'App',
  components: {
    PokemonCard,
  }

}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

body{
  background-color: rgb(73, 114, 190);
}
</style>
