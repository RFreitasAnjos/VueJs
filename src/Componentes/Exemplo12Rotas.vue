<script setup>
    import { ref,computed } from 'vue';

    import Pagina1 from './Pagina1.vue';
    import Pagina2 from './Pagina2.vue';
    import PaginaErro from './PaginaErro.vue';

    // Cria uma estrutura de rotas, contendo o caminho e o componente
    const routes = {
        '/': Pagina1,
        '/pagina2':Pagina2,
        '/404': PaginaErro
    }
    //Obter o conteudo a partir cerquila, exemplo: http://localhost:5173/#/sobre
    const referenciaRota = ref(window.location.hash)

    //Executa a acao quando realiza a navegacao entre paginas
    window.addEventListener('hashchange', () =>{
        referenciaRota.value = window.location.hash
    });

    // funcao responsavel por exibir a pagina especifica
    const currentView = computed(() =>{
        return routes[referenciaRota.value.slice(1) || '/' || PaginaErro]
    });
    
</script>

<template>
    <a href="#/">Pagina 1</a>
    <a href="#/pagina2">Pagina 2</a>

    <component :is="currentView"/>
</template>