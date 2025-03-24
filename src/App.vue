<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios'; 
import Tabla from './components/tabla.vue';
import Formulario from './components/formulario.vue';
import formularioper from './components/formularioper.vue';
import Tabla2 from './components/tabla2.vue';

const encabezados = ["id", "nombre", "edad", "habilidad", "origen", "descripcion"];
const contenido = ref([]);

async function mostrar() {
    try {
        const response = await axios.get('http://localhost:3000/api/personajes');
        console.log(response.data);
        contenido.value = response.data.filter(personaje => personaje.id !== 1);
    } catch (error) {
        console.error('Error al obtener datos:', error);
        contenido.value = [];
    }
}

onMounted(mostrar);

const encabezados1 = ["id", "nombre", "edad", "fecha_registro", "rol", "activo"];
const contenido1 = ref([]);

async function mostrarpar() {
    try {
        const response = await axios.get('http://localhost:3000/api/participantes');
        console.log(response.data);
        contenido1.value = response.data.filter(participante => participante.id !== 1);
    } catch (error) {
        console.error('Error al obtener datos:', error);
        contenido1.value = [];
    }
}

onMounted(mostrarpar);

const Eliminado = async (id) => {
    try {
        await axios.delete(`http://localhost:3000/api/personajes/${id}`);
        await mostrar(); 
    } catch (error) {
        console.error('Error al eliminar el personaje:', error);
    }
};

const Eliminado1 = async (id) => {
    try {
        await axios.delete(`http://localhost:3000/api/participantes/${id}`);
        await mostrarpar(); 
    } catch (error) {
        console.error('Error al eliminar el participante:', error);
    }
};
</script>

<template>
    <Formulario @actualizado="mostrar" />
    <Tabla :encabezados="encabezados" :contenido="contenido" @eliminado="Eliminado" />
    <formularioper />
    <Tabla2 :encabezados1="encabezados1" :contenido1="contenido1" @eliminado1="Eliminado1" /> 
</template>
