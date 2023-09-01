<script setup>
    const props = defineProps(['listaDeTarefas'])
</script>

<template>
    <ul v-if="props.listaDeTarefas.length" class="list-group mt-4">
        <li v-for="tarefa in props.listaDeTarefas" class="list-group-item">
            <input type="checkbox" :checked="tarefa.finalizada" :id="tarefa.titulo"
                @change="evt => tarefa.finalizada = evt.target.checked">
            <label :class="{ finished: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
        </li>
    </ul>
    <p v-else>Não há tarefas pendentes</p>
</template>

<style scoped>
.finished {
  text-decoration: line-through;
}
</style>