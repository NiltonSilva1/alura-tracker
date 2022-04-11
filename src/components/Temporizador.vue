<template>
  <div class="is-flex is-align-items-center is-justify-content-space-between">
    <Cronometro :tempoEmSegundos="tempoEmSegundos" />
    <button class="button" @click="iniciar">
      <span class="icon" v-if="cronometroRodando === false">
        <i class="fas fa-play"></i>
      </span>
      <span v-if="cronometroRodando === false">play</span>
      <span class="icon" v-if="cronometroRodando === true">
        <i class="fas fa-pause"></i>
      </span>
      <span v-if="cronometroRodando === true">pause</span>
    </button>
    <button
      class="button"
      @click="stop"
      :disabled="cronometroRodando === false"
    >
      <span class="icon">
        <i class="fas fa-stop"></i>
      </span>
      <span>stop</span>
    </button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Cronometro from "./Cronometro.vue";

export default defineComponent({
  name: "Temporizador-app",
  emits: ["aoTemporizadorFinalizado"],
  components: { Cronometro },

  data() {
    return {
      tempoEmSegundos: 0,
      cronometro: 0,
      cronometroRodando: false,
    };
  },
  methods: {
    iniciar() {
      // começar a contagem
      // 1 seg = 1000 ms
      if (this.cronometroRodando === false) {
        this.cronometroRodando = true;
        this.cronometro = setInterval(() => {
          this.tempoEmSegundos++;
        }, 1000);
      } else {
        this.cronometroRodando = false;
        clearInterval(this.cronometro);
      }
    },
    stop() {
      clearInterval(this.cronometro);
      this.cronometro = 0;
      this.cronometroRodando = false;
      this.$emit("aoTemporizadorFinalizado", this.tempoEmSegundos);
      this.tempoEmSegundos = 0;
    },
  },
});
</script>

<style></style>
