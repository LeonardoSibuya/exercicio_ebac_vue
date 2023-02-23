<script setup>
import { reactive } from 'vue';

const numeros = reactive({
  filtro: 'somar',
  numeroUm: 0,
  numeroDois: 0,
})

function somar() {
  const {numeroUm, numeroDois} = numeros;
  return Number(numeroUm) + Number(numeroDois) 
}

function subtrair() {
  const {numeroUm, numeroDois} = numeros;
  return Number(numeroUm) - Number(numeroDois)
}

function multiplicar() {
  const {numeroUm, numeroDois} = numeros;
  return Number(numeroUm) * Number(numeroDois)
}

function dividir() {
  const {numeroUm, numeroDois} = numeros;
  if (numeroUm && numeroDois > 0) {
    return numeroUm / numeroDois
  } else {
    return 0
  }
}

const resultado = () => {
  const { filtro } = numeros;

  switch (filtro) {
    case 'subtrair': 
      return subtrair();
    case 'multiplicar': 
      return multiplicar();
    case 'dividir':
      return dividir()
    default: 
      return somar()
  } 
}

</script>

<template>
  <div class="container">
    <header class="header">
      <h1 class="header__title">
        Calculadora Aritmética
      </h1>
    </header>
    <section class="calculadora">
      <input class="calculadora__input" type="number" placeholder="Insira aqui um número" @keyup="evento => numeros.numeroUm = evento.target.value">
      <select class="calculadora__select" @change="evento => numeros.filtro = evento.target.value">
        <option value="somar">+</option>
        <option value="subtrair">-</option>
        <option value="multiplicar">x</option>
        <option value="dividir">/</option>
      </select>
      <input class="calculadora__input" type="number" placeholder="Insira aqui outro número" @keyup="evento => numeros.numeroDois = evento.target.value">
      <span class="calculadora__resposta">
        {{ resultado() }}
      </span>
    </section>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.container {
  max-width: 960px;
  margin: 0 auto;
  background-color: lightgray;
  border-radius: 24px;
  font-family: sans-serif;
}

.header {
  text-align: center;
  padding: 24px 0;
  margin-bottom: 24px;
}

.header__title {
  font-size: 36px;
}

.calculadora {
  padding-bottom: 24px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.calculadora__input {
  margin: 0px 16px;
  padding: 8px;
  border: none;
  outline: none;
  font-size: 16px;
  background-color: #b6e1f0;
  border-radius: 8px;
}

.calculadora__input::-webkit-inner-spin-button {
  -webkit-appearance: none;
}

.calculadora__select {
  font-size: 16px;
  font-weight: bold;
  height: 30px;
  border-radius: 8px;
  border: none;
  outline: none;
  background-color: #b6e1f0;
}

.calculadora__resposta {
  display: block;
  font-size: 24px;
  font-weight: bold;
}

</style>
