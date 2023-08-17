<template>
  <header>
    <h1>
      <img src="../assets/logo-modavest.svg" alt="" />
    </h1>
    <button class="button" @click="alterarTema">
      {{ textoBotao }}
    </button>
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
  computed: {
    textoBotao() {
      if (this.modoEscuroAtivo) {
        return "Desativar modo escuro";
      }
      return "Ativar modo escuro";
    },
  },
  methods: {
    alterarTema() {
      this.modoEscuroAtivo = !this.modoEscuroAtivo;
      this.$emit("aoTemaAlterado", this.modoEscuroAtivo);
    },
  },
});
</script>

<style scoped>
/*todo o estilo do compomente*/
header {
  background: #2d004b;
  width: 104%;
  height: 100vh;
  text-align: center;
}
img {
  align-items: center;
  padding: 2rem;
}
@media only screen and (max-width: 760px) {
  header {
    padding: 2.5rem;
    height: auto;
  }
}
</style>
