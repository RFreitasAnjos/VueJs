<script setup>
    function validaFormulario(event){
        alert('Formulario enviado!');

        event.preventDefault();
    }
</script>

<template>
    <form action="http://www.ralflima.com" @submit="validaFormulario">
        <input type="submit" value="Enviar Formulario">
    </form>
</template>