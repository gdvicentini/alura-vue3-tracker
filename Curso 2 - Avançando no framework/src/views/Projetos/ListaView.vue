<template>
  <section>
    <router-link to="/projetos/novo" class="button">
      <span class="icon is-small">
        <i class="fas fa-plus"></i>
      </span>
    </router-link>
    <table class="table is-fullwidth">
      <thead>
        <th>ID</th>
        <th>Nome</th>
        <th>Ações</th>
      </thead>
      <tbody>
        <tr v-for="projeto in projetos" :key="projeto.id">
          <td>{{ projeto.id }}</td>
          <td>{{ projeto.nome }}</td>
          <td>
            <router-link :to="`/projetos/${projeto.id}`" class="button">
              <span class="icon is-small">
                <i class="fas fa-pencil-alt"></i>
              </span>
            </router-link>
            <button class="button ml-2 is-danger" @click="excluir(projeto.id)">
                <span class="icon is-small">
                    <i class="fas fa-trash"></i>
                </span>
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </section>
</template>

<script lang='ts'>
import { EXCLUIR_PROJETO } from "@/store/tipo-mutacoes";
import { computed, defineComponent } from "vue";
import { useStore } from "vuex";

export default defineComponent({
  name: "ListaView",
  methods: {
    excluir(id: string) {
        this.store.commit(EXCLUIR_PROJETO, id)
    }
  },
  setup() {
    const store = useStore();
    return {
      projetosSetup: computed(() => store.state.projetos),
      store
    };
  },
});
</script>