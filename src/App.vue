<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

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
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>

    <Formulario :tarefa-temp="estado.tarefaTemp" :cadastrar-tarefa="cadastrarTarefa" :trocar-filtro="evento => estado.filtro = evento.target.value" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value"/>

    <ListaDeTarefas :tarefas="getTarefasFiltradas()"/>

  </div>

</template>


