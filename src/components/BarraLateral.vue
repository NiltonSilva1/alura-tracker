<template>
  <header>
    <h1>
      <img src="../assets/logo.png" alt="Imagem logo" />
    </h1>
    <div class="darkMode">
      <button
        class="button is-success is-selected"
        @click="alterarTema"
        :disabled="modoEscuroAtivo === true"
      >
        Yes
      </button>
      <button class="button">Dark Mode</button>
      <button
        class="button is-danger is-selected"
        @click="alterarTema"
        :disabled="modoEscuroAtivo === false"
      >
        No
      </button>
    </div>
  </header>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "BarraLateral",
  emits: ["aoTemaAlterado"],
  data() {
    return {
      modoEscuroAtivo: false,
    };
  },
  methods: {
    alterarTema() {
      this.modoEscuroAtivo = !this.modoEscuroAtivo;
      this.$emit("aoTemaAlterado", this.modoEscuroAtivo);
    },
  },
});
</script>

<style>
header {
  padding: 1rem;
  background: #0d3b66;
  width: 100%;
  height: 100vh;
  text-align: center;
}

@media only screen and (max-width: 768px) {
  header {
    padding: 2.5rem;
    height: auto;
  }
}
</style>
