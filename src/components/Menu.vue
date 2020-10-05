<template>
  <div class="menu">
     <b-button pill id="btnExibirTodos" class="btnCustom mb-4" @click="exibirAll" v-show="!exibirTodos">Exibir Todos</b-button>
     <b-button pill id="btnOcultarTodos" class="btnCustom mb-4" @click="exibirAll" v-show="exibirTodos"> Voltar</b-button>
  </div>
</template>

<script>
export default {
    data(){
      return {
        exibirTodos: false
      }
    },

    methods: {
      exibirAll(event){
      if(event.target.id === "btnExibirTodos"){
         this.exibirTodos = true 
      } else {
        this.exibirTodos = false
      }
       this.$emit("btnExibir", { btnShowMenu: this.exibirTodos})
      }
    }
}
</script>

<style>
  .menu .btnCustom{
    font-family: 'Cabin', sans-serif;
    background: #193441;
  }
</style>