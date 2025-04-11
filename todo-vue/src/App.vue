<script setup>
  import { reactive } from "vue";
  import HeaderC from './components/HeaderC.vue';
  import Formulary from './components/Formulary.vue';
  import ToDoList from './components/ToDoList.vue';

  const estado = reactive({

    filtro: 'all',
    tarefaTemp: '',

    tarefas: [
      
    ]
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada);
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada);
  }

  const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch (filtro) {
      case 'pending':
        return getTarefasPendentes();
      case 'done':
        return getTarefasFinalizadas();
      default:
        return estado.tarefas;
    }
  }

  const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = '';
  }

  const getFiltro = () => estado.filtro;
</script>

<template>
  <div class="container">
    
    <HeaderC :tarefas-pendentes="getTarefasPendentes().length"/>

    <Formulary 
      :trocar-filtro="evento => estado.filtro = evento.target.value" 
      :tarefa-temp="estado.tarefaTemp" 
      :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" 
      :cadastra-tarefa="cadastraTarefa"/>

    <ToDoList 
      :trocar-filtro="evento => estado.filtro = evento.target.value" 
      :tarefas="getTarefasFiltradas()"
      
    />
    
  </div>
</template>

