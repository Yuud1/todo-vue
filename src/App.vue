<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [],
});

const getTarefasPendentes = () => estado.tarefas.filter(tarefa => !tarefa.finalizada);
const getTarefasFinalizadas = () => estado.tarefas.filter(tarefa => tarefa.finalizada);

const getTarefasFiltradas = () => {
  switch (estado.filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
};

const cadastrarTarefa = () => {
  if (estado.tarefaTemp.trim()) {
    const novaTarefa = { titulo: estado.tarefaTemp, finalizada: false };
    estado.tarefas.push(novaTarefa);
    estado.tarefaTemp = '';
  }
};

const alternarTarefa = (tarefa) => {
  tarefa.finalizada = !tarefa.finalizada;
};
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :estado="estado" @adicionar-tarefa="cadastrarTarefa" />
    <ListaDeTarefas :tarefas="getTarefasFiltradas()" @alternar-tarefa="alternarTarefa" />
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
