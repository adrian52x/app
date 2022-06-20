<template>
    
<h1>Pokemon App</h1>
<h2>Selected pokemon: <i>{{firstLetterUpperCase(pokemon)}}</i></h2> 
<div class="header">

<PokemonImage @updateSelected="updatePokeomonData" imgPath="images/Ditto.png" pokemonName="ditto"/>
<PokemonImage @updateSelected="updatePokeomonData" imgPath="images/Pikachu.jpg" pokemonName="pikachu"/>
<PokemonImage @updateSelected="updatePokeomonData" imgPath="images/charmander.jpg" pokemonName="charmander"/>

</div> 

    <div class="container">
       
        <div>
            <ul>
                <h3>Abilities</h3>
                <li v-for="ability in abilities" :key="ability">{{firstLetterUpperCase(ability.ability.name)}}</li>
            </ul>
        </div>

        <div>
            <ul>
                <h3>Stats</h3>
                <li v-for="stat in stats" :key="stat">{{firstLetterUpperCase(stat.stat.name)}}: {{stat.base_stat}}</li>
            </ul>
        </div>

        <div>
            <ul>
                <h3>Moves</h3>
                <li v-for="move in moves.slice(0,5)" :key="move"> {{firstLetterUpperCase(move.move.name)}} </li>
            </ul>
        </div>

    </div>
</template>

<script>

import PokemonImage from './PokemonImage.vue'

export default {
    name: 'PokemonCard',
    components: {
       PokemonImage
        
    }, 
    data: () =>({
        pokemon: 'pikachu',
        abilities: [],
        stats: [],
        moves: []
    }),

    async mounted(){
        this.updatePokeomonData();
        
    },
    methods: {
        firstLetterUpperCase: function (text){
            return text.charAt(0).toUpperCase() + text.slice(1)
        },
        
        async fetchData(pokemon){
                const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${pokemon}`)
                const data = await response.json();
            
                
                this.abilities = data.abilities;
                this.stats =  data.stats;
                this.moves =  data.moves;

                console.log(data.species.name);
                console.log(data);
        },

        async updatePokeomonData(newPokemon) {

            //Default
            if(newPokemon == undefined){
                
                this.fetchData(this.pokemon);


            }else{

                this.pokemon = newPokemon;
                this.fetchData(this.pokemon);
     
            }


           
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
.container{
    text-align: left;
    margin-top: 20px;
    margin-left: 10%;
    margin-right: 10%;
    background: rgb(255, 255, 255);
   
    display: grid;
    grid-template-columns: auto auto auto;
    border-radius: 15px;
}

</style>
