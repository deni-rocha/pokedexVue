<template>
  <div id="app">
    <div class="container">
      <h1 class="tittle mb-5"> POKEBOOK</h1>
    <b-input-group  class="mb-5">
      <b-input-group-prepend is-text>
        <b-icon icon="search" @click="buscar"></b-icon>
      </b-input-group-prepend>
      <b-form-input type="search" placeholder="pesquisar pokémon" v-model="busca" @keyup.enter="buscar"></b-form-input>
    </b-input-group>

      <div class="row">
        <div  v-for="(poke,index) in filteredPokemons" :key="poke.url" class="col">
        <Pokemond :name="poke.name" :url="poke.url" :num="index +1"/>
      </div>
      </div>
      
    </div>
  </div>
</template>

<script>
 import Pokemond from './components/Pokemon'
 import axios from 'axios';
export default {
  name: 'App',
  data(){
    return{
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },
  created: function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res => {
      this.pokemons = res.data.results
      this.filteredPokemons = res.data.results
    })
  },
  components: {
   Pokemond
  },
   computed: {
  //  resultadoBusca: function(){
  //    if(this.busca == '' || this.busca == ' '){
  //      return this.pokemons;
  //    } else {
  //      return this.pokemons.filter(pokemon => pokemon.name == this.busca)
  //    }
  //  }
 },
 methods: {
   buscar: function(){
     this.filteredPokemons = this.pokemons;
     if(this.busca == '' || this.busca == ' '){
       this.filteredPokemons = this.pokemons;
     } else {
       this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
     }
   }
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
.tittle {
  color: #F9FCF3;
  text-shadow: black 2px 4px 7px ;
  font-family: 'Cabin', sans-serif;
}
.txtBuscar{
  color: white;
  font-family: 'Cabin', sans-serif;
  text-shadow: black 2px 2px 2px ;
}
#input-default {
  border-radius: 2em;
}
</style>
