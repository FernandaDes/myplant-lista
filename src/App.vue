<template>
  <main class="columns is-gapless is-multiline" :class="{ 'modo-escuro' : modoEscuroAtivo }">
    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAlterado="trocarTema"/>
    </div>
        
    <div class="column is-three-quarter conteudo">
    <div class="lista">
      <FormularioUsuario @aoSalvarTarefa="salvarTarefa"/>
      
      <TarefaUser v-for="(tarefa,index) in tarefas" :key="index" :tarefa="tarefa"/>
      <BoxUser v-if="listaEstaVazia">
        Você ainda não plantou nada hoje :(
      </BoxUser>
    </div>
  </div>
</main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';
import BoxUser from './components/BoxUser.vue';
import FormularioUsuario from './components/FormularioUsuario.vue';
import TarefaUser from './components/TarefaUser.vue';
import IntTarefas from './interfaces/IntTarefa'
import Module from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { myPlantCOnfigService } from './config/db.myplant';

@Module({
  imports:[
    ConfigModule.forRoot({
      isGlobal: true
    }),
    TypeOrmModule.forRootAsync({
      useClass: myPlantCOnfigService,
      inject: [myPlantCOnfigService]
    })
  ]
})

export default defineComponent({
  name: 'App',
  components: {
    BarraLateral,
    FormularioUsuario,
    TarefaUser,
    BoxUser
},
  data(){
    return {
      tarefas: [] as IntTarefas[],
      modoEscuroAtivo: false
    }
  },
  computed: {
    listaEstaVazia () :boolean {
      return this.tarefas.length === 0
    }
  },
  methods:{
    salvarTarefa (tarefa: IntTarefas){
      this.tarefas.push(tarefa)
    },
    trocarTema (modoEscuroAtivo: boolean){
      this.modoEscuroAtivo = modoEscuroAtivo

    }
  }
});
</script>

<style>
.lista{
  padding: 1.25rem;
}
main {
  --bg-primario: #fff;
  --texto-primario:#000;

}
main.modo-escuro {
  --bg-primario: rgb(2, 25, 2);
  --texto-primario: #fff;
}
.conteudo {
  background-color: var(--bg-primario);
}

</style>
