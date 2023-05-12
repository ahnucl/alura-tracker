<template>
  <main class="columns is-gapless is-multiline">
    <div class="column is-one-quarter">
      <BarraLateral />
    </div>
    <div class="column is-three-quarter">
      <Formulario @aoSalvarTarefa="salvarTarefa"/>
      <div class="lista">
        <Tarefa 
          v-for="(tarefa, index) in tarefas" 
          v-bind:key="index"
          :tarefa="tarefa"
        />
        <Box v-if="listaEstaVazia">
          Você não está muito produtivo hoje :(
        </Box>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import BarraLateral from "./components/BarraLateral.vue"
import Formulario from "./components/Formulario.vue"
import Tarefa from "./components/Tarefa.vue"
import Box from "./components/Box.vue"
import type { ITarefa } from "./interfaces/ITarefa";

interface State {
  tarefas: ITarefa[]
}

export default defineComponent({
  name: 'App',
  components: {
    BarraLateral,
    Formulario,
    Tarefa,
    Box
  },
  data(): State {
    return {
      tarefas: [],
    }
  },
  computed: {
    listaEstaVazia() {
      return this.tarefas.length === 0
    }
  },
  methods: {
    salvarTarefa (tarefa: ITarefa) {
      this.tarefas.push(tarefa)
    }
  }
})
</script>

<style>
.lista {
  padding: 1.25rem;
}
</style>
