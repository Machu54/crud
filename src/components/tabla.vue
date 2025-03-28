<script setup>
import { ref } from "vue";

const props = defineProps({
    encabezados: Array, 
    contenido: Array 
});

const emit = defineEmits(["eliminado", "actualizar"]);
const mostrarModal = ref(false);
const personajeActual = ref({});

function eliminarPersonaje(id) {
    emit("eliminado", id);
}

function abrirModal(fila) {
    personajeActual.value = { ...fila };
    mostrarModal.value = true;
}

function actualizarPersonaje() {
    emit("actualizar", personajeActual.value);
    mostrarModal.value = false;
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
          <button @click="abrirModal(fila)">Editar</button>
          <button @click="eliminarPersonaje(fila.id)">Eliminar</button>
        </td>
      </tr>
    </tbody>
  </table>

  <div v-if="mostrarModal" class="modal">
    <div class="modal-contenido">
      <h2>Actualizar Personaje</h2>
      <label v-for="(valor, clave) in personajeActual" :key="'input-' + clave">
        {{ clave }}:
        <input v-model="personajeActual[clave]" />
      </label>
      <div class="botones">
        <button @click="actualizarPersonaje">Guardar</button>
        <button @click="mostrarModal = false">Cancelar</button>
      </div>
    </div>
  </div>
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

.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal-contenido {
  background: white;
  padding: 20px;
  border-radius: 10px;
}
.botones {
  margin-top: 10px;
  display: flex;
  justify-content: space-between;
}
</style>
