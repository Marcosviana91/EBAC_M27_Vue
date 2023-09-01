<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue'
import Formulario from './components/Formulario.vue'
import ListaDeTarefas from './components/ListaDeTarefas.vue'



const estado = reactive({
  tarefas: [
    {
      titulo: ' Estudar ES6',
      finalizada: false,
    },
    {
      titulo: ' Estudar SASS',
      finalizada: false,
    },
    {
      titulo: ' Academia',
      finalizada: true,
    },
  ],
  filtro: 'todas',
  novaTarefa: '',
})

const getTarefasFinalizadas = (estaFinalizada = true) => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada == estaFinalizada)
}

const getTarefasFiltradas = () => {
  const { filtro } = estado

  switch (filtro) {
    case 'pendentes':
      return getTarefasFinalizadas(false)
    case 'finalizadas':
      return getTarefasFinalizadas()
    default:
      return estado.tarefas
  }
}

const cadastrarTarefa = () => {
  const tarefa = {
    titulo: estado.novaTarefa,
    finalizada: false,
  }
  estado.tarefas.push(tarefa)
  estado.novaTarefa = ''
}
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasFinalizadas(false).length"/>

    <Formulario :cadastrar-tarefa="cadastrarTarefa" :nova-tarefa="estado.novaTarefa" :trocar-filtro="evt => estado.filtro = evt.target.value" :edita-nova-tarefa="evt => estado.novaTarefa = evt.target.value"/>

    <ListaDeTarefas :lista-de-tarefas="getTarefasFiltradas()"/>
  </div>
</template>

<style scoped>
</style>
