<script setup>
    const props = defineProps(['tarefasFiltradas'])
    // Emissor de eventos para o pai
    const emit = defineEmits(['atualizar-tarefa-finalizada']);

    // Função para emitir evento para o componente pai
    const marcarComoFinalizada = (tarefa) => {
        emit('atualizar-tarefa-finalizada', tarefa);
};
</script>
<template>
    <ul class="list-group mt-4">
    <li class="list-group-item" v-for="(tarefa, index) in props.tarefasFiltradas" :key="index">
        <input :checked="tarefa.finalizado" :id="'tarefa-' + index"  type="checkbox" @change="marcarComoFinalizada(tarefa)" >
        <label :class="{ done: tarefa.finalizado }" class="ms-3" :for="'tarefa-' + index" >
            {{tarefa.nome}}
        </label>
    </li>
</ul>
</template>
<style scoped>
    .done{
        text-decoration: line-through;
    }
</style>