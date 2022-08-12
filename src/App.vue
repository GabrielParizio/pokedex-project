<template>
  <div id="app">
   <div class="container">
    <h1 class="mb-4" align="middle">Pokemons</h1>
    <PokemonSearch
      :apiUrl="apiUrl" 
      @setPokemonUrl="setPokemonUrl"/>
      <PokemonLista
      @setPokemonUrl="setPokemonUrl"/>
      <PokemonDetail
      :pokemonUrl="pokemonUrl"
      v-if="showDetail"
      @closeDetail="closeDetail"/>
  
    </div>
   
    
  </div>
</template>

<script>

import PokemonLista from  './components/PokemonList.vue'
import PokemonDetail from './components/PokemonDetail.vue'
import PokemonSearch from './components/PokemonSearch.vue'
export default {
  data(){
    return{
      apiUrl: 'https://pokeapi.co/api/v2/pokemon/',
      pokemonUrl: '',
      showDetail: false,
    }
  },
components:{
  PokemonSearch,
  PokemonLista,
  PokemonDetail
},
methods:{
  setPokemonUrl(url){
    this.pokemonUrl= url;
    this.showDetail = true;
  },
  closeDetail(){
    this.pokemonUrl= '';
    this.showDetail = false;
  }
}
}
</script>

<style scoped>
 .container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 10px;
    width: calc(100% - 20px);
    min-height: calc(100vh - 20px);
    background: radial-gradient(#156F99, #0A2E50);
    font-family: 'Acme', arial;
    font-size: 1rem;
    font-weight: normal;
  }
  h1 { color: #efefef; }
</style>
