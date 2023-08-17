<template>
  <box-component>
    <div class="columns">
      <div class="column is-4">{{ tarefa.descricao || 'Tarefa sem descrição' }}</div>
      <div class="column is-3">{{ tarefa.projeto?.nome || 'N/D' }}</div>
      <div class="column">
        <cronometro-component :tempoEmSegundos="tarefa.duracaoEmSegundos" />
      </div>
    </div>
  </box-component>
</template>

<script lang="ts">
import ITarefa from "../interfaces/ITarefa";
import { defineComponent, PropType } from "vue";
import BoxComponent from "./BoxComponent.vue";
import CronometroComponent from "./CronometroComponent.vue";

export default defineComponent({
  components: { CronometroComponent, BoxComponent },
  name: "TarefasComponent",
  props: {
    tarefa: {
      type: Object as PropType<ITarefa>,
      required: true
    },
  },
  computed: {
    tempoGasto () : string {
      return new Date(this.tarefa.duracaoEmSegundos * 1000)
        .toISOString()
        .substr(11, 8)
    }
  }
});
</script>

<style scoped>
.box {
  background: #faf0ca;
}
</style>
