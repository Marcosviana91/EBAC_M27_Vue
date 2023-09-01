<script setup>

import { reactive } from 'vue';

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
    <header class="p-5 bm--4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>Você possui {{ getTarefasFinalizadas(false).length }} tarefas pendentes</p>
    </header>
    <form @submit.prevent="cadastrarTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.novaTarefa" @change="evt => estado.novaTarefa = evt.target.value" required class="form-control" type="text"
            placeholder="Digita a tarefa">
        </div>
        <div class="col-md-2">
          <button class="btn btn-primary">Inserir</button>
        </div>
        <div class="col-md-2">
          <select @change="evt => estado.filtro = evt.target.value" class="form-control">
            <option value="todas">Todas as tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li v-for="tarefa in getTarefasFiltradas()" class="list-group-item">
        <input type="checkbox" :checked="tarefa.finalizada" :id="tarefa.titulo"
          @change="evt => tarefa.finalizada = evt.target.checked">
        <label :class="{ finished: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.finished {
  text-decoration: line-through;
}
</style>
