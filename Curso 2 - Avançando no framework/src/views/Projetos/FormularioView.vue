<template>
  <section>
    <form @submit.prevent="salvar">
      <div class="field">
        <label for="nomeDoProjeto" class="label"> Nome do Projeto </label>
        <input
          type="text"
          class="input"
          v-model="nomeDoProjeto"
          id="nomeDoProjet"
        />
      </div>
      <div class="field">
        <button class="button" type="submit">Salvar</button>
      </div>
    </form>
  </section>
</template>

<script lang='ts'>
import { TipoNotificacao } from "@/interfaces/INotificacao";
import { ADICIONA_PROJETO, ALTERA_PROJETO } from "@/store/tipo-mutacoes";
import { defineComponent } from "vue";
import { useStore } from "vuex";
import useNotificador from "@/hooks/notificador"

export default defineComponent({
  name: "FormularioView",
  props: {
    id: { type: String }
  },
  mounted () {
    if (this.id) {
      const projeto = this.store.state.projetos.find((proj: any) => proj.id == this.id)
      this.nomeDoProjeto = projeto?.nome || ''
    }
  },
  data() {
    return {
      nomeDoProjeto: "",
    };
  },
  methods: {
    salvar() {
      if (this.id) {
        this.store.dispatch(ALTERA_PROJETO, {
          id: this.id,
          nome: this.nomeDoProjeto
        })
      } else {
        this.store.dispatch(ADICIONA_PROJETO, this.nomeDoProjeto)
      }
      this.nomeDoProjeto = "";
      this.notificar(TipoNotificacao.SUCESSO, 'Excelente!', 'O Projeto foi cadastrado com sucesso!')
      this.$router.push('/projetos')
    },
    
  },
  setup () {
    const store = useStore()
    const { notificar } = useNotificador()
    return {
      store,
      notificar
    }
  }
});
</script>

