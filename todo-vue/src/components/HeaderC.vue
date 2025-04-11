<script setup>
    const props = defineProps(['tarefasPendentes']);
</script>

<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>My tasks</h1>
        <p>
            You have {{ props.tarefasPendentes }} pending tasks.
        </p>
    </header>
</template>