<template>
<div>     
    <b-row>
      
    <b-col cols="3" v-for="(pokemon,index) in pokemons" :key="index">
      
      <b-card class="mb-2" bg-variant="dark">
        <b-row class="display-middle">
        <img
        :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${get_id(pokemon)}.png`" 
        :alt="pokemon.name"
        @click="setPokemonUrl(pokemon.url)" >
      <h3 class="text-center">{{get_name(pokemon)}}</h3>
      <h3></h3>
      </b-row>
      </b-card>
      </b-col>
  </b-row>
  </div>
</template>

<script>

import axios from "axios"

export default {
data(){
  return {
    pokemons: [],

    imgUrl: 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/',
    pokemonUrl:'',
    showDetail: false
  }
},
components:{
  
},
methods:{
    setPokemonUrl(url){
    this.$emit('setPokemonUrl',url)
  },
  get_id(pokemon){
    return Number(pokemon.url.split("/")[6])
  },
  get_name(pokemon){
    return pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1)
  },

  
},
mounted() {
  axios.get('https://pokeapi.co/api/v2/pokemon?limit=151')
    .then((response)=>
      {
        this.pokemons = response.data.results
        }
    )
  
}
}
</script>

<style scoped>
h3{color:aliceblue}

</style>