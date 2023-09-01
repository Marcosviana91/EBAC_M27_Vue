<script setup>
    const props = defineProps(['cadastrarTarefa', 'novaTarefa', 'trocarFiltro', 'editaNovaTarefa'])
</script>

<template>
    <form @submit.prevent="props.cadastrarTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.novaTarefa" @change="props.editaNovaTarefa" required
                    class="form-control" type="text" placeholder="Digita a tarefa">
            </div>
            <div class="col-md-2">
                <button class="btn btn-primary">Inserir</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    <option value="todas">Todas as tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>