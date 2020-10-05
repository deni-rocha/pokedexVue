<template>
  <b-container class="cardPokemon">
          <b-card
            no-body
            style="max-width: 10rem; min-width: 200px;"
            :img-src="currentImg"
            img-alt="Image"
            img-top
            class="mr-auto ml-auto mb-4"
          >
            <template v-slot:header>
              <h4 class="mb-0">{{name}}</h4>
            </template>

            <b-card-body>
              <b-card-sub-title class="mb-2">{{pokemon.type}}</b-card-sub-title>
            </b-card-body>
        <b-list-group flush>
      <b-list-group-item><b-button @click="mudarSprite" id="btnCustom">Mudar Visualização</b-button></b-list-group-item>
    </b-list-group>

           
          </b-card>
  </b-container>
</template>

<script>

import axios from 'axios';
export default {
  created: function(){
    axios.get(this.url).then(res =>{
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default
      this.pokemon.back = res.data.sprites.back_default
      this.currentImg = this.pokemon.front
    })
  },
  data(){
    return {
      isFront: true,
      currentImg: '',
      pokemon: {
        type: "",
        front: "",
        back: ""      }
    }
  },
  props: {
    name: String,
    url: String,
    num: Number
  },
  filters: {
  upper: function(value){
    let newName = value[0].toUpperCase() + value.slice(1);
    return newName
 } },
 methods: {
   mudarSprite: function(){
     if(this.isFront){
       this.currentImg = this.pokemon.back;
       this.isFront = false
     } else {
       this.isFront = true;
       this.currentImg = this.pokemon.front;
     }
   }
 }
}
</script>

<style>
   #btnCustom{
    background: #193441;
  }
</style>