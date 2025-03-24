<script setup>
import axios from "axios";

const props = defineProps({
    encabezados: Array, 
    contenido: Array 
});

const emit = defineEmits(['eliminado']);

function eliminarPersonaje(id) {
  emit("eliminado", id);
}
</script>

<template>
  <table class="tabla">
    <thead>
      <tr>
        <th v-for="(titulo, index) in props.encabezados" :key="'th-' + index">
          {{ titulo }}
        </th>
        <th>Acciones</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(fila, indexFila) in props.contenido" :key="'fila-' + indexFila">
        <td v-for="(valor, clave) in fila" :key="'td-' + indexFila + '-' + clave">
          {{ valor }}
        </td>
        <td>
          <button>Editar</button>
          <button @click="eliminarPersonaje(fila.id)">Eliminar</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<style scoped>
.tabla {
  border: 2px solid black;
  width: 100%;
  border-collapse: collapse;
}

th, td {
  border: 2px solid black;
  text-align: center;
  padding: 8px;
}
button {
  border: 2px solid black;
  margin-right: 5px;
  padding: 5px 10px;
  cursor: pointer;
}
</style>
