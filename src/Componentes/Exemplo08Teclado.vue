<script setup>
    function mensagem(){
        alert('Executando a funçao');
    }
</script>

<template>
    <input type="text" @keyup.enter="mensagem()">
</template>