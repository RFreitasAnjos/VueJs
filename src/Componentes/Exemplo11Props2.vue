<script setup>
    const props = defineProps(['nome', 'idade','cidade','vetor','funcao']);
</script>
<template>
    <p>Nome: {{ nome }}</p>
    <p>Idade: {{ idade }}</p>
    <p>Cidade: {{ cidade }}</p>
    <ul>
        <li v-for="cidade of vetor">{{cidade}}</li>
    </ul>

    <button @click="funcao">Clique Aqui</button>
</template>