<script setup>
const props = defineProps(['tarefas']);
const emit = defineEmits(['alternar-tarefa']);
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas" :key="tarefa.titulo">
            <input 
                type="checkbox" 
                :checked="tarefa.finalizada" 
                :id="tarefa.titulo" 
                @change="emit('alternar-tarefa', tarefa)"
            />
            <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
            {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>
