<script setup>
import {ref} from 'vue';


  const msg="Vengo desde un script setup";
  const colorH2= "color: yellow";
  const arrayColores=["red","blue","green"];
  const activo= null;
  const arrayFrutas= [{nombre: "manzana", precio: 1.2, descripcion: "Fruta roja y jugosa"},{nombre: "pera", precio: 0.5, descripcion: "Fruta blanca y crujiente"},{nombre: "naranja", precio: 1.5, descripcion: "Fruta naranja y refrescante"}];
  const objetoFruta= {nombre: "kiwi", precio: 2.0, descripcion: "Fruta verde y exótica"};
//Metodos
const handleClick=(Message)=>{ console.log(Message) }

const counter = ref (0);
const increment = () => { console.log(counter.value++) } 
const reset = () => { console.log(counter.value = 0) }

</script>

<template>
  <h1>{{ msg.toUpperCase() }}</h1>
  <h2 :style="`color: ${arrayColores[1]}`">usando V-BIND</h2>
  <p  :style=colorH2 > {{activo ? "Estoy activado" : "Estoy desactivado"}}</p>
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

  <button @click="increment">Incrementar</button>
  <button @click="reset">Resetear</button>
  <p>Contador: {{counter}}</p>

</template>

<style>
  h1{color: red;
  }
</style>
