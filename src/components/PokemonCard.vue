<template>
    
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



export default {
    name: 'PokemonCard',
    components: {
       
        
    }, 
    data: () =>({
        pokemon: 'pikachu',
        abilities: [],
        stats: [],
        moves: []
    }),

    async mounted(){
        const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${this.pokemon}`)
        const data = await response.json();
    
        
        this.abilities = data.abilities;
        this.stats =  data.stats;
        this.moves =  data.moves;


        console.log(data.species.name);
        console.log(data);
    },
    methods: {
        firstLetterUpperCase: function (text){
            return text.charAt(0).toUpperCase() + text.slice(1)
        },

        updatePokeomon(variable) {
        this.pokemon = variable
        }
    }

  
}


</script>


<style scoped>
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
