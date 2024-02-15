<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  productos: {
    type: Array,
    default: () => []
  }
})

const tacharProducto = (producto) => {
  producto.comprado = !producto.comprado
}

const mostrarImportantes = ref(false)

const productosFiltrados = computed(() => {
  return mostrarImportantes.value
    ? props.productos.filter((producto) => producto.importante)
    : props.productos
})
</script>

<template>
  <label>
    <input v-model="mostrarImportantes" type="checkbox" />
    Mostrar solo los más importantes
  </label>
  <ul>
    <li
      v-for="producto in productosFiltrados"
      :key="producto.id"
      :class="{
        'es-importante': producto.importante,
        tachado: producto.comprado
      }"
      @click="tacharProducto(producto)"
    >
      {{ producto.nombre }} - {{ producto.id }}
    </li>
  </ul>
</template>

<style>
.es-importante {
  color: red;
}

.tachado {
  text-decoration: line-through;
}
</style>
