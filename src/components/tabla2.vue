<script setup>
import axios from "axios";
const props = defineProps({
    encabezados1: Array, 
    contenido1: Array
});

const emit = defineEmits(['eliminado1']);

function eliminarparticipante(eliminar){
  emit("eliminado1", eliminar )
}

</script>

<template>
  <table class="tabla">
    <thead>
      <tr>
        <th v-for="(titulo, index) in props.encabezados1" :key="'th-' + index">
          {{ titulo }}
        </th>
        <th>Acciones</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(fila, indexFila) in props.contenido1" :key="'fila-' + indexFila">
        <td v-for="(info, indexInfo) in fila" :key="'td-' + indexFila + '-' + indexInfo">
          {{ info }}
        </td>
        <td>
          <button>Editar</button>
          <button @click="eliminarparticipante(fila.id)">Eliminar</button>
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