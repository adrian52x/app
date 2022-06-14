<template>
  <div class="circle">
    <img v-bind:alt="pokemonName" v-bind:src="imgPath" v-on:click="selectPokemon(pokemonName)">
  </div>
  
 
</template>

<script>


export default {
  name: 'PokemonImage',
  props: {
    imgPath: String,
    pokemonName: String
  },
  methods: {
    selectPokemon: function(value){
      this.$emit('updateSelected', value)
       
    }
  }
  
}
</script>


<style scoped>

img {
    height: 200px;
    width: 200px;
    border-radius: 80%;
    
}
.circle{
    height: 200px;
    width: 200px;
    background: rgb(255, 255, 255);
    border-radius: 50%;
}

</style>
