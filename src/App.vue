<!-- LOGICA - JavaScript -->
<script setup>
//importamos la librería ref y computed
import { ref, computed } from 'vue'
const name = "VUE DINÁMICO";

// ahora counter es una variable reactiva
const counter = ref(0);
const arrayFavoritos = ref([]);

// se le agrega el .value si es una variable reactiva
const increment = () => { counter.value++; }
const decrease = () => { counter.value--; }
const reset = () => { counter.value = 0; }
const add = () => {
  arrayFavoritos.value.push(counter.value)
}

// recibe una función de flecha y siempre tiene que retornar algo
const classCounter = computed(() => {
  if (counter.value === 0) {
    return 'zero';
  }
  if (counter.value > 0) {
    return 'positive';
  }
  if (counter.value < 0) {
    return 'negative';
  }
})

const bloquearBtnAdd = computed(() => {
  const numSearch = arrayFavoritos.value.find(num => num === counter.value)
  console.log(numSearch);
  // if(numSearch === 0)return true;
  // return numSearch ? true : false;
  return numSearch || numSearch === 0
})
</script>

<!-- ESTRUCTURA - Sintaxis de pantilla -->
<template>
  <div class="container text-center mt-3">
    <h1>Hola {{ name.toUpperCase() }}!!!</h1>
    <h1>Hola MIAMOR!</h1>

    <!-- no es necesario agregar el .value en el template -->
    <h2 :class="classCounter">{{ counter }}</h2>
    <div class="btn-group">
      <button @click="increment" class="btn btn-primary">Aumentar</button>
      <button @click="decrease" class="btn btn-danger">Disminuir</button>
      <button @click="reset" class="btn btn-secondary">Resetear</button>
      <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">Agregar</button>
    </div>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="(num, index) in arrayFavoritos" :key="index">
        {{ num }}
      </li>
    </ul>
  </div>
</template>

<!-- ESTILOS -->
<style>
h1 {
  color: purple;
}

.positive {
  color: green;
}

.negative {
  color: red;
}

.zero {
  color: peru;
}
</style>
