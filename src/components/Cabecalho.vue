<script setup>
    const props = defineProps(['tarefasPendentes'])
</script>

<template>
    <header class="p-5 bm--4 mt-4 bg-light rounded-3">
        <h1>Minhas tarefas</h1>
        <p>Você possui {{ props.tarefasPendentes }} tarefas pendentes</p>
        <!-- <p>Você possui {{ getTarefasFinalizadas(false).length }} tarefas pendentes</p> -->
    </header>
</template>