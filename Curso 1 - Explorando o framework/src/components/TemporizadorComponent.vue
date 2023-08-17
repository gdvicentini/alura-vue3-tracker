<template>
  <section class="is-flex is-align-items-center is-justify-content-space-between">
    <cronometro-component :tempoEmSegundos="tempoEmSegundos" />
    <botao-component
      @clicado="iniciar"
      icone="fas fa-play"
      texto="play"
      :desabilitado="cronometroRodando"
    />
    <botao-component
      @clicado="finalizar"
      icone="fas fa-stop"
      texto="stop"
      :desabilitado="!cronometroRodando"
    />
  </section>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import BotaoComponent from "./BotaoComponent.vue";
import CronometroComponent from "./CronometroComponent.vue";

export default defineComponent({
  components: { CronometroComponent, BotaoComponent },
  name: "TemporizadorComponent",
  emits: ["aoTemporizadorFinalizado"],
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
      this.cronometroRodando = true;
      this.cronometro = setInterval(() => {
        this.tempoEmSegundos += 1;
      }, 1000);
    },
    finalizar() {
      this.cronometroRodando = false;
      clearInterval(this.cronometro);
      this.$emit("aoTemporizadorFinalizado", this.tempoEmSegundos);
      this.tempoEmSegundos = 0;
    },
  },
});
</script>
