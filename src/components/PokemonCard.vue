<template>
    
<h1>Pokemon App</h1>

<h2 >Selected pokemon: <i>{{input}}</i></h2> 


<div class="search-container">
    <img class="search-icon" src="data:image/svg+xml;utf8;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iaXNvLTg4NTktMSI/Pgo8IS0tIEdlbmVyYXRvcjogQWRvYmUgSWxsdXN0cmF0b3IgMTkuMC4wLCBTVkcgRXhwb3J0IFBsdWctSW4gLiBTVkcgVmVyc2lvbjogNi4wMCBCdWlsZCAwKSAgLS0+CjxzdmcgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayIgdmVyc2lvbj0iMS4xIiBpZD0iQ2FwYV8xIiB4PSIwcHgiIHk9IjBweCIgdmlld0JveD0iMCAwIDU2Ljk2NiA1Ni45NjYiIHN0eWxlPSJlbmFibGUtYmFja2dyb3VuZDpuZXcgMCAwIDU2Ljk2NiA1Ni45NjY7IiB4bWw6c3BhY2U9InByZXNlcnZlIiB3aWR0aD0iMTZweCIgaGVpZ2h0PSIxNnB4Ij4KPHBhdGggZD0iTTU1LjE0Niw1MS44ODdMNDEuNTg4LDM3Ljc4NmMzLjQ4Ni00LjE0NCw1LjM5Ni05LjM1OCw1LjM5Ni0xNC43ODZjMC0xMi42ODItMTAuMzE4LTIzLTIzLTIzcy0yMywxMC4zMTgtMjMsMjMgIHMxMC4zMTgsMjMsMjMsMjNjNC43NjEsMCw5LjI5OC0xLjQzNiwxMy4xNzctNC4xNjJsMTMuNjYxLDE0LjIwOGMwLjU3MSwwLjU5MywxLjMzOSwwLjkyLDIuMTYyLDAuOTIgIGMwLjc3OSwwLDEuNTE4LTAuMjk3LDIuMDc5LTAuODM3QzU2LjI1NSw1NC45ODIsNTYuMjkzLDUzLjA4LDU1LjE0Niw1MS44ODd6IE0yMy45ODQsNmM5LjM3NCwwLDE3LDcuNjI2LDE3LDE3cy03LjYyNiwxNy0xNywxNyAgcy0xNy03LjYyNi0xNy0xN1MxNC42MSw2LDIzLjk4NCw2eiIgZmlsbD0iIzAwMDAwMCIvPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8L3N2Zz4K" />
    <input class="search-bar" type="text" v-model="input" placeholder="Search.." name="search" >
    <button class="submit-btn" type="submit" v-on:click="fetchData(input.toLowerCase())" v-bind:disabled="isDisabled(input)" >Submit</button>
</div>


<div v-if="hasActiveInfo" class="header">

    <PokemonImage  v-bind:imgPath="imgUrl" />
   

</div> 

    <div v-if="hasActiveInfo" class="container">
       
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
        input: '',
        hasActiveInfo: false,
        abilities: [],
        stats: [],
        moves: [],
        imgUrl: ''
    }),

    async mounted(){
    
    },
    methods: {
        firstLetterUpperCase: function(text){
            return text.charAt(0).toUpperCase() + text.slice(1)
        },
        isDisabled(input) {
            
            return input.length === 0;

        },
        
        async fetchData(pokemon){
            try {
                const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${pokemon}`)
                const data = await response.json();
                    
                this.abilities = data.abilities;
                this.stats =  data.stats;
                this.moves =  data.moves;
                this.imgUrl = data.sprites.front_default;

                this.hasActiveInfo = true;
                    
                this.$toast.success(`Hey! we found: `+ pokemon);

                

                console.log(data);

            } catch (error) {
                
                this.$toast.error(`Hey! no pokemon found: `+ pokemon);
                console.log(error);
            }
                
        }

    }

  
}


</script>


<style scoped>

.search-container{
    padding-bottom: 30px;
    position: relative;
    display: flex;
    justify-content: center;
    
}
.search-icon {
    position: relative;
    left: 25px;
    width: 18px;
}
.search-bar {
    border: 1px solid grey;
    border-radius: 5px;
    height: 35px;
    width: 25%;
    padding: 2px 23px 2px 30px;
    outline: 0;
    background-color: #f5f5f5;
    border-radius: 15px;
}

.submit-btn {
    position: relative;
    
    right: 55px;
    
    border: 1px solid;
    border-top-right-radius: 15px;
    border-bottom-right-radius: 15px;
    
}

.submit-btn:hover {
    cursor: pointer;
    background-color: #60a1b4;
    transition: 0.3s;
}


.header {
    display: flex;
    align-items: center;
    justify-content: center;
    
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
