<script setup>
const props = defineProps(['cadastrarTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp']);
</script>

<template>
    <form @submit.prevent="props.cadastrarTarefa" class="mb-4">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required type="text" placeholder="Digite aqui a Descrição da tarefa" class="form-control" />
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    <option value="todas">Todas Tarefas</option>
                    <option value="pendentes">Tarefas Pendentes</option>
                    <option value="concluidas">Tarefas Concluídas</option>
                </select>
            </div>
        </div>
    </form>
</template>