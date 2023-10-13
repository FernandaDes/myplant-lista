
import BoxUser from './BoxUser.vue';
<template>
  <BoxUser>
    <div class="columns">
      <div class="column is-7">
       {{ tarefa.descricao || 'Tarefa sem descrição'}}
      </div>
    <div class="column">
      <CronometroPlanta :tempoEmSegundos="tarefa.duracaoEmSegundos" />

    </div>
    </div>
  </BoxUser>
</template>

<script lang="ts">
import IntTarefa from '@/interfaces/IntTarefa';
import { defineComponent, PropType } from 'vue'
import CronometroPlanta from './CronometroPlanta.vue'
import BoxUser from './BoxUser.vue';

export default defineComponent ({
  name: 'TarefaUser',
  components: {
    CronometroPlanta,
    BoxUser
},
  props:{
    tarefa: {
      type: Object as PropType<IntTarefa>,
      required: true
    }
  }
})

</script>

