<script setup>   
  import { reactive } from "vue";
  import Cabecalho from "./components/Cabecalho.vue";
  import Formulario from "./components/Formulario.vue";
  import ListaDeTarefas from "./components/ListaDeTarefas.vue";

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
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario 
      :tarefas-novas="cadastrarTarefaNova" 
      :tarefa-temp="evento => estado.tarefaTemp = evento.target.value" 
      :evento-filtro="evento => estado.filtro = evento.target.value"
    />
    <ListaDeTarefas :tarefas-filtradas="getTarefasFiltradas()" @atualizar-tarefa-finalizada="toggleFinalizado"/>
    
    
  </div>
  
</template>

<style scoped>
  .done{
    text-decoration: line-through;
  }
</style>
