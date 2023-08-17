<template>
  <box-component>
    <div class="columns">
      <div class="column is-7">{{ tarefa.descricao }}</div>
      <div class="column">
        <cronometro-component :tempoEmSegundos="tarefa.duracaoEmSegundos" />
      </div>
    </div>
  </box-component>
</template>

<script lang="ts">
import ITarefa from "@/interfaces/ITarefa";
import { defineComponent, PropType } from "vue";
import BoxComponent from "./BoxComponent.vue";
import CronometroComponent from "./CronometroComponent.vue";

export default defineComponent({
  components: { CronometroComponent, BoxComponent },
  name: "TarefasComponent",
  props: {
    tarefa: {
      type: Object as PropType<ITarefa>,
    },
  },
});
</script>

<style scoped>
.box {
  background: #faf0ca;
}
</style>
