<script setup>
  import { reactive } from "vue";

  const estado = reactive({

    filtro: 'all',
    tarefaTemp: '',

    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada: false,
      },
      {
        titulo: 'Estudar SASS',
        finalizada: false,
      },
      {
        titulo: 'Ir para a academia',
        finalizada: true,
      },
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
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>My tasks</h1>
      <p>
        You have {{ getTarefasPendentes().length }} pending tasks.
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">

        <div class="col">

          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required type="text" class="form-control" placeholder="Type here the task description">

        </div>
        <div class="col-md-1">

          <button type="submit" class="btn btn-primary">Add</button>

        </div>
        <div class="col-md-2">

          <select @change="evento => estado.filtro = evento.target.value" class="form-control">

            <option value="all">All tasks</option>
            <option value="pending">Pending tasks</option>
            <option value="done">Done tasks</option>

          </select>

        </div>

      </div>
    </form>

    <ul class="list-group mt-4">

      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">

        <input @change="evento => tarefa.finalizada = evento.target.checked"  :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>

      </li>
    </ul>
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>