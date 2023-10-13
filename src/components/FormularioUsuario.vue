<template>
<div class="box formulario">
  <div class="columns">
    <div class="column is-6" role="form" aria-label="Qual planta você quer saber mais?">
      <input 
        type="text" 
        class="input" 
        placeholder="Que planta você quer conhecer?"
        v-model="descricao">

    </div>
    <div class="column">
      <Temporizador @ao-temporizador-finalizado="finalizarTarefa"/>
    </div>
  </div>
</div>



</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Temporizador from './Temporizador.vue'


export default defineComponent({
  nome:'formularioUsuario',
  emits:['aoSalvarTarefa'],
  components:{
    Temporizador
  },
data(){
  return{
    descricao: ''
  }
},

methods:{
  finalizarTarefa(tempoDecorrido: number): void {
    this.$emit('aoSalvarTarefa', {
      duracaoEmSegundos: tempoDecorrido,
      descricao: this.descricao
       })
    this.descricao =''

  }
}

});
</script>

<style>
.formulario {
  color: var(--texto-primario);
  background-color: var(--bg-primario);
}


</style>