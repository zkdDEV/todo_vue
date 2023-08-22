<script setup>
    // Definindo as propriedades que vão ser pegas do app.vue
    const props = defineProps(['tarefasPendentes'])
</script>

<template>
    <header class="p-5 mb-5 mt-5 bg-light rounded-3">
        <h1>Minhas titulos</h1>
        <p>
            Você possuí {{ props.tarefasPendentes }} tarefas pendentes
        </p>
    </header>
</template>