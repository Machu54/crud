<script setup>
import { ref } from "vue";

const props = defineProps({
    encabezados1: Array, 
    contenido1: Array
});

const emit = defineEmits(["eliminado1", "actualizar2"]);
const mostrarModal = ref(false);
const participanteActual = ref({});

function eliminarparticipante(id) {
    emit("eliminado1", id);
}

function abrirModal(fila) {
    participanteActual.value = { ...fila };
    mostrarModal.value = true;
}

function actualizarParticipante() {
    emit("actualizar", participanteActual.value);
    mostrarModal.value = false;
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
          <button @click="abrirModal(fila)">Editar</button>
          <button @click="eliminarparticipante(fila.id)">Eliminar</button>
        </td>
      </tr>
    </tbody>
  </table>

  <div v-if="mostrarModal" class="modal">
    <div class="modal-contenido">
      <h2>Actualizar Participante</h2>
      <label v-for="(valor, clave) in participanteActual" :key="'input-' + clave">
        {{ clave }}:
        <input v-model="participanteActual[clave]" />
      </label>
      <div class="botones">
        <button @click="actualizarParticipante">Guardar</button>
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
