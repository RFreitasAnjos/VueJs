<script setup>
    let nomes = ['Alice','Bruna','Carla','Daniela','Elen']
</script>
<template>
    <ul>
        <li v-for="pessoa in nomes">{{ pessoa }}</li>
    </ul>
</template>