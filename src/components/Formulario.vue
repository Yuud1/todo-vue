<script setup>
const props = defineProps(['estado']);
const emit = defineEmits(['adicionar-tarefa']);

const handleSubmit = () => {
    emit('adicionar-tarefa');
};
</script>

<template>
    <form @submit.prevent="handleSubmit">
        <div class="row">
            <div class="col">
                <input v-model="estado.tarefaTemp" required type="text" placeholder="Digite a descrição da tarefa" class="form-control">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select v-model="estado.filtro" class="form-control">
                    <option value="todas">Todas as tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>

<style scoped>
</style>
