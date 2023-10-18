<template>
  <div class="cep">
    <h1>Busca Endereco pelo CEP</h1>
    <input v-model="cep" placeholder="Digite o CEP" />
    <button @click="buscarEndereco">Buscar</button>
    <pre v-if="resultado">{{ resultado }}</pre>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .cep {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  .cep * {
    margin-bottom: 1rem;
  }
}
</style>

<script setup>
import { ref } from 'vue'

const cep = ref('13871298')
const resultado = ref('')

function hasValidCEP() {
  return cep.value.trim()
}

async function buscarEndereco() {
  if (hasValidCEP()) {
    const apiUrl = import.meta.env.VITE_API_CEP + cep.value + '/json/'

    try {
      const resposta = await fetch(apiUrl)
      resultado.value = await resposta.json()
    } catch (erro) {
      resultado.value = 'Erro ao buscar o CEP'
    }
  }
}
</script>
