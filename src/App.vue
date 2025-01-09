<template>
<div class="w-full h-full flex justify-center items-center">
    <div v-if="chiste">
      <div style="background-color: #db3434; color: #ffffff; border-radius: 7px;">{{ chiste.setup }}</div>
      <div>Clica ↓aqui↓ para saber</div>
      <template v-if="escon">
        <div style="background-color: #db3434; color: #ffffff; border-radius: 7px;">{{ chiste.delivery }}</div>
        <div>Clica ↓aqui↓ para otro</div>
        <button style="background-color: #3498db; color: #3498db; border-radius: 7px;" @click="definirchistemalo2">Another</button>
      </template>
      <button style="background-color: #3498db; color: #3498db; border-radius: 7px;" v-else @click="mostrarchis">Tell Me!</button>
    </div>
  </div>
</template>

<script setup>
//fucnion para variables cambiables
import { ref } from 'vue';
//establecer variables
const chiste = ref(null);
const escon = ref(false);
//buscar el chiste de el link
async function buscarchistemalo() {
  const san = await window.fetch('https://v2.jokeapi.dev/joke/christmas?type=twopart');
  const json = await san.json();
  return json;
}

async function definirchistemalo() {
  const sans = await buscarchistemalo();
  chiste.value = sans;
}

function mostrarchis() {
  escon.value = true;
}

function definirchistemalo2() {
  chiste.value = null;
  escon.value = false;
  definirchistemalo();
}

definirchistemalo();
</script>

