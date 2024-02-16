<script setup>
    let texto = '<p style="color:red">Aprendendo a diretiva v-html</p>';
</script>
<template>
    <div v-html="texto"></div> <!-- Ao utilizar a diretiva v-html tem a possibildiade de usar tag, diferentemente da interpolaçao--> 
    <div>{{ texto }}</div>
</template>
