<script setup>
import { reactive } from 'vue';

const estado = reactive({
  filtro: 'todas',
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
      titulo: 'Estudar CSS',
      finalizada: false,
    },
    {
      titulo: 'Estudar HTML',
      finalizada: true,
    }
  ]
})

const getTarefasPendentes = () =>
{
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () =>
{
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getTarefasFiltradas = () =>
{
  const { filtro } = estado
  switch(filtro)
  {
    case 'pendentes':
      return getTarefasPendentes()
    case 'finalizadas':
      return getTarefasFinalizadas()
    default:
      return estado.tarefas
  }
}

const cadastraTarefa = () =>
{
  const tarefaNova =
  {
    titulo: estado.tarefaTemp,
    finalizada: false
  }
  estado.tarefas.push(tarefaNova)
  estado.tarefaTemp = ''
}
</script>

<template>
  <div class="container">
    <header class="p-5 mb-5 mt-5 bg-light rounded-3">
      <h1>Minhas titulos</h1>
      <p>
        Você possuí {{ getTarefasPendentes ().length}} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" placeholder="Digite qual vai ser a tarefa" type="text" required class="form-control">
        </div>
        <div class="col-md-2">
          <button class="btn btn-primary">
            Cadastrar
          </button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
    
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{done: tarefa.finalizada}" :for="tarefa.titulo" class="ms-3">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done
{
  text-decoration: line-through;
}
</style>
