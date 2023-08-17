<template>

      <formulario-component @aoSalvarTarefa="salvarTarefa" />
      <div class="lista">
        <box-component v-if="listaEstaVazia">
          Você não está muito produtivo hoje :(
        </box-component>
        <!-- Lista de tarefas -->
        <tarefas-component
          v-for="(tarefa, index) in tarefas"
          :key="index"
          :tarefa="tarefa"
        />
      </div>

</template>

<script lang="ts">
import { defineComponent } from "vue";
import BoxComponent from "../components/BoxComponent.vue";
import FormularioComponent from "../components/FormularioComponent.vue";
import TarefasComponent from "../components/TarefasComponent.vue";
import ITarefa from "../interfaces/ITarefa";

export default defineComponent({
  components: {
    FormularioComponent,
    TarefasComponent,
    BoxComponent,
  },
  name: "TarefasView",
  data() {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false,
    };
  },
  computed: {
    listaEstaVazia(): boolean {
      return this.tarefas.length == 0;
    },
  },
  methods: {
    salvarTarefa(tarefa: ITarefa) {
      this.tarefas.push(tarefa);
    },
    trocarTema(modoEscuroAtivo: boolean) {
      this.modoEscuroAtivo = modoEscuroAtivo;
    },
  },
});
</script>

<style>
.lista {
  padding: 1.25rem;
}
main {
  --bg-primario: #fff;
  --texto-primario: #000;
}
main.modo-escuro {
  --bg-primario: #2b2d42;
  --texto-primario: #ddd;
}
.conteudo {
  background-color: var(--bg-primario);
}
</style>
