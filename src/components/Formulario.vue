<script setup>
const { tarefasNovas, tarefaTemp, eventoFiltro } = defineProps([
    'tarefasNovas',
    'tarefaTemp',
    'eventoFiltro'
]);
</script>

<template>
    <form @submit.prevent="tarefasNovas">
        <div class="row">
            <div class="col">
                <input 
                @input="tarefaTemp" 
                type="text" 
                placeholder="Digite aqui a descrição da tarefa" 
                class="form-control"
                />
            </div>
            <div class="col-md-2">
            <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="eventoFiltro" class="form-control">
                    <option value="Todas">Todas tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Concluídas</option>
                </select>
            </div>
        </div>
    </form>
</template>