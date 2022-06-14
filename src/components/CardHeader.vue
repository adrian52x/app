<template>
<h1>Pokemon App</h1>
<h2>Selected pokemon: <i>{{selectedPokemon}}</i></h2> 
<div class="header">

<PokemonImage @updateSelected="updatePokeomon" imgPath="images/Ditto.png" pokemonName="Ditto"/>
<PokemonImage @updateSelected="updatePokeomon" imgPath="images/Pikachu.jpg" pokemonName="Pikachu"/>
<PokemonImage @updateSelected="updatePokeomon" imgPath="images/charmander.jpg" pokemonName="Charmander"/>

</div> 


  
  
</template>

<script>
import PokemonImage from './PokemonImage.vue'

export default {
    name: 'CardHeader',
    
    data: () => ({
    selectedPokemon: 'Pikachu',
    }),

    components: {
      PokemonImage
        
    },
    methods: {
    updatePokeomon(value) {
        this.selectedPokemon = value;
    }
}
    

    
}
</script>


<style scoped>

.header {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
 
}

</style>
