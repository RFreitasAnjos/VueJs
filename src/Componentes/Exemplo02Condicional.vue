<script setup>
    let exibir = true;
    let nota1 = 10;
    let nota2 = 5;
    let media = (nota1 + nota2) / 2;
</script>
<template>
    <p v-if="exibir">To aqui</p>
    <p v-if="media >= 7">Aprovado(a)</p>
    <p v-else-if="media >= 5">Em exame</p>
    <p v-else>Reprovado</p>
</template>