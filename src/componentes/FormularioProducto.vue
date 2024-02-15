<script setup>
import {ref} from 'vue'
const emits = defineEmits(['agregar'])

const productoNuevo = ref('')
const esImportante = ref(false)

const agregarALaLista = () => {
    emits('agregar',{ nombre : productoNuevo.value, importante : esImportante.value})
    productoNuevo.value=""
    esImportante.value=false
}

</script>


<template>
    <form class="add-item-form" @submit.prevent="agregarALaLista">
    <input
      v-model="productoNuevo"
      type="text"
      placeholder="Que quieres comprar?"
    />
    <label>
      <input v-model="esImportante" type="checkbox" />
      Muy importante
    </label>
    <button class="btn btn-primary">Añadir producto</button>
  </form>
</template>
