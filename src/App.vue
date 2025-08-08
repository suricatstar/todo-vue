<script setup>
import { reactive } from 'vue';


const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas : [
        {
            titulo: 'Estudar Vue.js',
            concluida: false
        },
        {
            titulo: 'Estudar N8N',
            concluida: false
        },
        {
            titulo: 'Ir Caminhar',
            concluida: true
        }
    ]
})

const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.concluida);
}

const getTarefasConcluidas = () => {
    return estado.tarefas.filter(tarefa => tarefa.concluida);
}

const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch (filtro) {
        case 'todas':
            return estado.tarefas;
        case 'pendentes':
            return getTarefasPendentes();
        case 'concluidas':
            return getTarefasConcluidas();
        default:
            return estado.tarefas;
    }

}
const cadastrarTarefa = () => {
    

    const tarefaNova = {
        titulo: estado.tarefaTemp,
        concluida: false
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = '';
}
</script>

<template>

  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>Minhas tarefas</h1>
        <p>Você possui {{ getTarefasPendentes().length }} tarefas pendentes</p>
    </header>

    <form @submit.prevent="cadastrarTarefa" class="mb-4">
        <div class="row">
            <div class="col">
                <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required type="text" placeholder="Digite aqui a Descrição da tarefa" class="form-control" />
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="evento => estado.filtro = evento.target.value" class="form-control">
                    <option value="todas">Todas Tarefas</option>
                    <option value="pendentes">Tarefas Pendentes</option>
                    <option value="concluidas">Tarefas Concluídas</option>
                </select>
            </div>
        </div>
    </form>

    {{ estado.filtro }}

    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
            <input @change="evento => tarefa.concluida = evento.target.checked" type="checkbox" class="form-check-input me-1" :checked="tarefa.concluida" :id="tarefa.titulo"/>
            <label :class="{'done': tarefa.concluida}" class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>

        </li>
    </ul>

  </div>

</template>

<style scoped>
    .done{
        text-decoration: line-through;
    }
</style>
