<script setup>
import { ref, computed, watch } from 'vue';

const num1 = ref(0);
const num2 = ref(0);
const operacao = ref('soma');

const validarNumero = (numero) => {
  return numero < 0 ? 0 : numero;
};

watch(num1, (novoValor) => {
  num1.value = validarNumero(novoValor);
});

watch(num2, (novoValor) => {
  num2.value = validarNumero(novoValor);
});

const resultado = computed(() => {
  let result = 0;
  switch (operacao.value) {
    case 'soma':
      result = parseFloat(num1.value) + parseFloat(num2.value);
      break;
    case 'subtracao':
      result = parseFloat(num1.value) - parseFloat(num2.value);
      break;
    case 'multiplicacao':
      result = parseFloat(num1.value) * parseFloat(num2.value);
      break;
    case 'divisao':
      result = parseFloat(num1.value) / parseFloat(num2.value);
      break;
  }
  return isNaN(result) ? 'Inválido' : result;
});
</script>

<template>
<div>
    <input type="number" v-model="num1" placeholder="Digite o primeiro número" />
    <select v-model="operacao">
      <option value="soma">+</option>
      <option value="subtracao">-</option>
      <option value="multiplicacao">*</option>
      <option value="divisao">/</option>
    </select>
    <input type="number" v-model="num2" placeholder="Digite o segundo número" />
    <h2>Resultado: {{ resultado }}</h2>
  </div>
</template>

<style scoped>
input, select {
  margin: 10px;
  padding: 5px;
}
</style>
