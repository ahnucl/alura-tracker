<template>
  <button class="button" @click="onClick" :disabled="desabilitado">
      <span class="icon">
        <i :class="fullIconName"></i>
      </span>
      <span>{{ texto }}</span>
    </button>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

  export default defineComponent({
    name: 'Botao',
    props: {
      icone: {
        type: String
      },
      texto: {
        type: String
      },
      desabilitado: {
        type: Boolean,
        default: false
      }
    },
    emits: ['click'],
    methods: {
      onClick() {
        this.$emit('click')
      }
    },
    computed: {
      fullIconName() {
        return `fas ${this.icone}`
      }
    }
  })

</script>