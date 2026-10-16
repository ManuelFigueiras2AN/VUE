<script setup>

import {ref, computed} from 'vue';


  const msg="Vengo desde un script setup";
  const colorH2= "color: yellow";
  const arrayColores=["red","blue","green"];
  const activo= null;
  const arrayFrutas= [{nombre: "manzana", precio: 1.2, descripcion: "Fruta roja y jugosa"},{nombre: "pera", precio: 0.5, descripcion: "Fruta blanca y crujiente"},{nombre: "naranja", precio: 1.5, descripcion: "Fruta naranja y refrescante"}];
  const objetoFruta= {nombre: "kiwi", precio: 2.0, descripcion: "Fruta verde y exótica"};

  //Metodos
const handleClick=(Message)=>{ console.log(Message) }

const counter = ref (0);
const increment = () => { counter.value++ } 
const decrement = () => { counter.value-- }
const reset = () => (counter.value = 0)
const add = () => { arrayNumerosFav.value.push(counter.value) }

const counterClass = computed(() =>{
  
  if (counter.value > 0) 
  { return "positivo" }
  
  if (counter.value < 0) 
  { return "negativo" }
  
  else 
  { return "zero" } } )

  const arrayNumerosFav=ref([]);
  const controlNumberFav= computed(()=>{
  const numberBlocked= arrayNumerosFav.value.find((number) => number === counter.value);
  if (numberBlocked === 0)
  { return true }
  return numberBlocked ? true : false
   //return numberBlocked || numberBlocked === 0 =>> Solucion mas optima de código, ya que el find devuelve el valor del elemento encontrado y si es 0, 
   // lo considera como false, por eso se hace la comparacion con 0 para que devuelva true en ese caso. 
  });

</script>

<template>
  <h1>{{ msg.toUpperCase() }}</h1>
  <h2 :style="`color: ${arrayColores[1]}`">usando V-BIND</h2>
  <p  :style= colorH2 > {{activo ? "Estoy activado" : "Estoy desactivado"}}</p>
  <h2 :style="`color: ${arrayColores[2]}`" v-if="activo === true"> Estoy activo con VUE</h2>
  <h2 :style="`color: ${arrayColores[0]}`" v-else-if="activo === false"> Estoy desactivado con VUE</h2>
  <h2 :style="`color: ${arrayColores[1]}`" v-else> Estoy en null </h2>
  <ul>
    <li v-for="(fruta,index) of arrayFrutas" :key="fruta.nombre" > {{++index}}. {{fruta.nombre}} - ${{fruta.precio}} - {{fruta.descripcion}}</li>
  </ul>
  <ul>
    <li v-for= "(value,propiedad,index) of objetoFruta" :key="propiedad"> {{++index}}. {{propiedad}} : {{value}}</li>
  </ul>

  <button @click="handleClick('Click desde el boton')">Click</button>
  <button @click.right.prevent="handleClick('Click derecho desde el boton')">Click derecho</button>
  <button @click.middle="handleClick('Click medio desde el boton')">Click medio</button>
  <button @click.left ="handleClick('Click izquierdo desde el boton')">Click izquierdo</button>


  <p :class=counterClass> Contador: {{counter}}</p>
  <button @click="increment">Incrementar</button>
  <button @click="reset">Resetear</button>
  <button @click="decrement">Decrementar</button>
  <button @click="add" :disabled="controlNumberFav">Agregar numero</button>
  
  <ul>
    <li v-for="(numero,index) of arrayNumerosFav" :key="index"> {{++index}}. {{numero}}</li>
  </ul>
  
</template>

<style>
  h1{color: red;}
  .positivo{color: green;}
  .negativo{color: red;}
  .zero{color: yellow;}
</style>
