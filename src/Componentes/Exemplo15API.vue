<script setup>
// Importações
import "bulma/css/bulma.min.css";
import { onMounted, ref } from "vue";

// Variáveis reativas
let produtos = ref([]);

let btnCadastro = ref(true);

let obj = ref({
  produto: "",
  valor: 0,
});

// Busca a lista de produtos quando o componente é montado
onMounted(() => {
  fetch("http://localhost:3000/produtos")
    .then((requisicao) => requisicao.json())
    .then((retorno) => (produtos.value = retorno));
});

/*----------------------------------------------------------------*/

// Função de cadastro
function cadastrar(event) {
  // Atribui um ID ao objeto antes de enviar
  obj.value.id = produtos.value.length + 1;

  // Envia o objeto para o servidor
  fetch("http://localhost:3000/produtos", {
    method: "POST",
    body: JSON.stringify(obj.value),
    headers: { "Content-Type": "application/json" },
  })
    .then((req) => req.json())
    .then((res) => {
      // Adiciona o produto retornado pelo servidor à lista de produtos
      produtos.value.push(res);

      // Limpa o objeto
      obj.value.produto = "";
      obj.value.valor = 0;
    });

  // Impede o recarregamento da página
  event.preventDefault();
  alert("Produto Cadastrado");
}

function editar() {
  fetch("http://localhost:3000/produtos/" + obj.value.id, {
    method: "PUT",
    body: JSON.stringify(obj.value),
    headers: { "Content-Type": "application/json" },
  })
    .then((requisicao) => requisicao.json())
    .then((retorno) => {
      // Adiciona o produto retornado pelo servidor à lista de produtos
      let indice = produtos.value.findIndex((objP) => {
        return objP.id === retorno.id;
      });

      produtos.value[indice] = retorno;

      // Limpa o objeto
      obj.value.id = 0;
      obj.value.produto = "";
      obj.value.valor = 0;
    });

  alert("Produto Alterado");
}

function excluir() {
  fetch(`http://localhost:3000/produtos/${obj.value.id}`, {
    method: "DELETE",
    headers: { "Content-Type": "application/json" },
  })
    .then((requisicao) => requisicao.json())
    .then(() => {
      let indice = produtos.value.findIndex((objP) => {
        return objP.id === obj.value.id;
      });
      produtos.value.splice(indice, 1);
      btnCadastro.value = true;

      obj.value.id = 0;
      obj.value.produto = "";
      obj.value.valor = 0;
    });
}

// Função para selecionar um produto
function Select(indice) {
  obj.value = {
    id: produtos.value[indice].id,
    produto: produtos.value[indice].produto,
    valor: produtos.value[indice].valor,
  };

  btnCadastro.value = false;
}
</script>

<!--CSS -->
<style>
form {
  width: 50%;
  display: flex;
  flex-flow: column nowrap;
  margin: 0 auto;
  text-align: center;
}
input {
  margin-bottom: 5px;
}
</style>

<template>
  <form @submit="cadastrar">
    <!--<p>{{ obj }}</p>-->
    <input type="hidden" v-model="obj.id" />
    <input
      type="text"
      placeholder="Produto"
      class="form"
      v-model="obj.produto"
    />
    <input type="number" placeholder="Valor" class="form" v-model="obj.valor" />
    <input type="submit" v-if="btnCadastro" value="Cadastrar" class="button" />
    <input
      type="button"
      @click="editar"
      v-if="!btnCadastro"
      value="Editar"
      class="button"
    />
    <input
      type="button"
      @click="excluir"
      v-if="!btnCadastro"
      value="Excluir"
      class="button"
    />
  </form>

  <table
    class="table is-bordered is-striped is-narrow is-hoverable is-fullwidth"
  >
    <thead>
      <tr>
        <th>Produto</th>
        <th>Valor</th>
        <th>Selecionar</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(p, indice) in produtos">
        <td>{{ p.produto }}</td>
        <td>{{ p.valor }}</td>
        <td>
          <button @click="Select(indice)" class="button">Selecionar</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>
