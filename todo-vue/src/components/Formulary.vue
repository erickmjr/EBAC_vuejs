<script setup>

    const props = defineProps([
        'cadastraTarefa', 
        'tarefaTemp',
        'trocarFiltro',
        'editaTarefaTemp'
    ]);
    
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">

                <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required
                    type="text" class="form-control" placeholder="Type here the task description">

            </div>
            <div class="col-md-1">

                <button type="submit" class="btn btn-primary">Add</button>

            </div>
            <div class="col-md-2">

                <select @change="props.trocarFiltro" class="form-control">
                    <option value="all">All tasks</option>
                    <option value="pending">Pending tasks</option>
                    <option value="done">Done tasks</option>
                </select>

            </div>
        </div>
    </form>
</template>