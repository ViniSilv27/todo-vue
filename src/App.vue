<script setup>   
  import { reactive } from "vue";
  const estado = reactive({
    filtro: 'Todas',
    tarefaTemp: '',
    tarefas:  [
      {
      nome: 'Ir à academia',
      finalizado: false
    },
    {
      nome: 'Estudar Full Estack Java - Ebac',
      finalizado: false
    },
    {
      nome: 'Almoçar saudavel',
      finalizado: false
    }
    
  ]
  })
  // NOVO: Método para alternar o status 'finalizado' da tarefa
  const toggleFinalizado = (tarefa) => {
    tarefa.finalizado = !tarefa.finalizado;
  // O Vue 3 com `reactive` tornará isos reativo e uatalizará a UI
  };

// NOVO: Exemplo de como você pode contar tarefas pendentes (para p o do cabeçalho)
  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizado);
  };
  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizado);
  };

  const getTarefasFiltradas = () => {
    const {filtro} = estado

    switch (filtro) {
      case 'pendentes':
        
        return getTarefasPendentes();

      case 'finalizadas':
        return getTarefasFinalizadas()
    
      default:
        return estado.tarefas;
    }
  }

  const cadastrarTarefaNova =  () => {
    const novaTarefa = {
      nome: estado.tarefaTemp,
      finalizado: false
    }
    estado.tarefas.push(novaTarefa)
  }
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>você possui {{ getTarefasPendentes().length }} tarefas pendentes</p>
    </header>
    <form @submit.prevent="cadastrarTarefaNova()">
    <div class="row">
      <div class="col">
        <input @change="evento => estado.tarefaTemp = evento.target.value" type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-primary">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change="evento => estado.filtro = evento.target.value" class="form-control">
          <option value="todas">Todas tarefas</option>
          <option value="pendentes">Pendentes</option>
          <option value="finalizadas">Concluidas</option>
        </select>
      </div>
    </div>
  </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="(tarefa, index) in getTarefasFiltradas()" :key="index">
        <input
          :checked="tarefa.finalizado"
          :id="'tarefa-' + index"  type="checkbox"
          @change="toggleFinalizado(tarefa)" >
        <label
          :class="{ done: tarefa.finalizado }" class="ms-3"
          :for="'tarefa-' + index" >
          {{tarefa.nome}}
        </label>
      </li>
    </ul>
  </div>
  
</template>

<style scoped>
  .done{
    text-decoration: line-through;
  }
</style>
