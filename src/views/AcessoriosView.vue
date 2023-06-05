<script>
import AcessoriosApi from "@/api/acessorios";
const acessoriosApi = new AcessoriosApi();
export default {
  data() {
    return {
      acessorios: [],
      acessorio: {},
    };
  },
  async created() {
    this.acessorios = await acessoriosApi.buscarTodosOsAcessorios();
  },
  methods: {
    async salvar() {
      if (this.acessorio.id) {
        await acessoriosApi.atualizarAcessorio(this.acessorio);
      } else {
        await acessoriosApi.adicionarAcessorio(this.acessorio);
      }
      this.acessorio = {};
      this.acessorios = await acessoriosApi.buscarTodosOsAcessorios();
    },
    editar(acessorio) {
      Object.assign(this.acessorio, acessorio);
    },
    async excluir(acessorio) {
      await acessoriosApi.excluirAcessorio(acessorio.id);
      this.acessorios = await acessoriosApi.buscarTodosOsAcessorios();
    },
  },
};
</script>

<template>
  <h1>Acessorios</h1>
  <hr />
  <div class="form">
    <input type="text" v-model="acessorio.descricao" placeholder="Descrição" />
    <button @click="salvar">Salvar</button>
  </div>
  <hr />
  <ul>
    <li v-for="acessorio in acessorios" :key="acessorio.id">
      <span @click="editar(acessorio)">
        ({{ acessorio.id }}) - {{ acessorio.descricao }} -
      </span>
      <button @click="excluir(acessorio)">X</button>
    </li>
  </ul>
</template>

<style></style>