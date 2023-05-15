<template>
  <div class="is-flex is-align-items-center is-justify-content-space-between">
    <Cronometro :tempo-em-segundos="tempoEmSegundos" />
    <Botao 
      icone="fa-play" 
      texto="play" 
      :desabilitado="cronometroRodando"
      @click="iniciar" 
    />
    <Botao 
      icone="fa-stop" 
      texto="stop" 
      :desabilitado="!cronometroRodando"
      @click="finalizar" 
    />
    
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Cronometro from './Cronometro.vue'
import Botao from './Botao.vue'

export default defineComponent({
  name: 'Temporizador',
  emits: ['ao-temporizador-finalizado'],
  components: {
    Cronometro, 
    Botao
  },
  data() {
    return {
      tempoEmSegundos: 0,
      cronometro: 0,
      // cronometroRodando: false
    }
  },
  methods: {
    iniciar() {
      this.cronometro = setInterval(() => {
        this.tempoEmSegundos += 1
      }, 1000)
      // this.cronometroRodando = true
    },
    finalizar() {
      clearInterval(this.cronometro)
      this.$emit('ao-temporizador-finalizado', this.tempoEmSegundos)
      this.tempoEmSegundos = 0
      this.cronometro = 0
    },
  },
  computed: {
    cronometroRodando() {
      return !!this.cronometro
    }
  }
})
</script>