<template>
  <div id="app">
    <div class="container">
      <h1 class="tittle mb-5 animate__animated" @click="effect"> POKEDEX</h1>
    <b-input-group  class="mb-5">
      <b-input-group-prepend is-text>
        <b-icon icon="search" @click="buscar"></b-icon>
      </b-input-group-prepend>
      <b-form-input type="search" placeholder="pesquisar pokémon" v-model="busca" @keyup.enter="buscar" @keyup.delete="buscar"></b-form-input>
    </b-input-group>

    <Menu @btnExibir="exibirAll($event)"/>
      <div class="row" v-if="exibirTodos">
        <div  v-for="(poke,index) in filteredPokemons" :key="poke.url" class="col">
        <Pokemond :name="poke.name" :url="poke.url" :num="index +1"/>
      </div>
      </div>

    </div>
  </div>
</template>

<script>
 import Menu from './components/Menu'
 import Pokemond from './components/Pokemon'
 import axios from 'axios';
export default {
  name: 'App',
  data(){
    return{
      pokemons: [],
      filteredPokemons: [],
      busca: '',
      exibirTodos: false
    }
  },
  created: function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res => {
      this.pokemons = res.data.results
      this.filteredPokemons = res.data.results
    })
  },
  components: {
   Pokemond,
   Menu
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
       this.filteredPokemons = ''
     } else {
       this.exibirTodos = true
       this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca.toLowerCase());
     }
   },
   exibirAll($event){
     if($event.btnShowMenu){
       this.exibirTodos = $event.btnShowMenu
       this.filteredPokemons = this.pokemons
     } else {
       this.filteredPokemons = ''
     }   
   },

   effect(event){
     
     setTimeout(function(){
       event.target.classList.remove('animate__flipInY')
       event.target.style.color = '#F9FCF3'
     }, 2000)
     event.target.style.color = '#ff0000'
     event.target.classList.add('animate__flipInY')
     
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
