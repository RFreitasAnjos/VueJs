<!--
    PROPS -> Propriedades.

    A utilizaçao de Props fornece uma comunicacao entre componentes,
    podemos enviar
-->
<script setup>
    import Exemplo11Props2 from './Exemplo11Props2.vue'

    let cidade = 'Recife';
    let cidades = ['Recife','Joao Pessoa','Natal','Fortaleza'];

    function mensagem(){
        alert('Funçao criada no componente: Exemplo11Props1')
    }
</script>

<template>
    <Exemplo11Props2 nome="Renan" idade="24" :cidade="cidade" :vetor="cidades" :funcao="mensagem()"></Exemplo11Props2>
</template>