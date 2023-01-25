<template>
  <div class="c-container">
    <header class="container__header">
      <h1 class="calc-title text-[2rem] font-bold">Vue Calculator</h1>
    </header>
    <div class="container__screen text-[2rem] font-bold">{{ result }}</div>
    <div class="container__buttons grid grid-cols-4 gap-4">
      <CalcButton  @updateScreen="updateScreen" text="7" value="7"></CalcButton>
      <CalcButton  @updateScreen="updateScreen" text="8" value="8"></CalcButton>
      <CalcButton  @updateScreen="updateScreen" text="9" value="9"></CalcButton>
      <StateButton @updateState="updateState" text="DEL" value="del"></StateButton>
      <CalcButton  @updateScreen="updateScreen" text="4" value="4"></CalcButton>
      <CalcButton  @updateScreen="updateScreen" text="5" value="5"></CalcButton>
      <CalcButton  @updateScreen="updateScreen" text="6" value="6"></CalcButton>
      <CalcButton  @updateScreen="updateScreen" text="+" value="+"></CalcButton>
      <CalcButton  @updateScreen="updateScreen" text="1" value="1"></CalcButton>
      <CalcButton  @updateScreen="updateScreen" text="2" value="2"></CalcButton>
      <CalcButton  @updateScreen="updateScreen" text="3" value="3"></CalcButton>
      <CalcButton  @updateScreen="updateScreen" text="-" value="-"></CalcButton>
      <CalcButton  @updateScreen="updateScreen" text="." value="."></CalcButton>
      <CalcButton  @updateScreen="updateScreen" text="0" value="0"></CalcButton>
      <CalcButton  @updateScreen="updateScreen" text="/" value="/"></CalcButton>
      <CalcButton  @updateScreen="updateScreen" text="x" value="x"></CalcButton>
      <StateButton @updateState="updateState" text="RESET" value="reset"></StateButton>
      <MemoryButton @updateMemory="updateMemory" text="M+" value="storeMemory"></MemoryButton>
      <MemoryButton @updateMemory="updateMemory" text="MC" value="clearMemory"></MemoryButton>
      <ResultButton @calculate="calculate"></ResultButton>
    </div>
  </div>
</template>

<script setup>
import CalcButton from './CalcButton.vue';
import StateButton from './StateButton.vue';
import ResultButton from './ResultButton.vue';
import MemoryButton from './MemoryButton.vue';
import { ref, onMounted } from '@vue/runtime-core';

const result = ref('0');

onMounted(() => {
  let storeData = localStorage.getItem('storedData')
  if (storeData !== null) {
    result.value = storeData;
  }else {
    result.value = '0'
  }
})

function updateMemory (value) {
  if (value !== 'clearMemory') {
    localStorage.setItem('storedData', result.value)
  }else {
    localStorage.removeItem('storedData')
    result.value = '0';
  }
}

function updateScreen (value) {
  result.value = result.value !== '0' ? result.value + value : value + '';
}

function updateState (value) {
  if (value) {
    if (value === 'reset') reset()
    else if (value === 'del') remove()
  }
}

function calculate () {
  if (verifyScreen()) {
    const str = result.value.replace('x', '*')
    result.value = eval(str) + ''
  } else console.log('error')
}

function verifyScreen () {
  const reg = /(?:(?:^|[-+_*/])(?:\s*-?\d+(\.\d+)?(?:[eE][+-]?\d+)?\s*))+$/
  const str = result.value.replace('x', '*')
  return reg.test(str)
}

function remove () {
  const length = result.value.length
  if (length - 1 > 0) result.value = result.value.substring(0, length - 1)
  else result.value = '0'
}

function reset () {
  result.value = '0';
}
</script>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
