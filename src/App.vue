<script setup>
import { ref } from 'vue'
import ListaProductos from './componentes/ListaProductos.vue'
import FormularioProducto from './componentes/FormularioProducto.vue';

const titulo = ref('Lista de la compra')
const productos = ref([])

const añadirALaLista = ({nombre,importante}) => {
  productos.value.push({
    id: productos.value.length + 1,
    nombre: nombre,
    importante: importante
  })
}

const todos =ref([])

async function pedirTodos(){
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/todos/`
  )
  todos.value = await res.json()
} 
pedirTodos()
</script>

<template>
  <h1>{{ titulo }}</h1>
  <FormularioProducto @agregar="añadirALaLista"/>
  <ListaProductos :productos="productos" />

  <p v-if="!productos.length">La lista está vacia</p>

  <ul>
    <li v-for="todo in todos">{{ todo.title }}</li>
  </ul>
</template>
