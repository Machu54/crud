<script setup>
import { ref, defineEmits } from "vue";
import axios from "axios";


const json = ref({
  nombre: "",
  edad: "",
  habilidad: "",
  origen: "",
  descripcion: ""
});


const emit = defineEmits(["actualizado"]);

const boton = async () => {
  const options = {
    method: "POST",
    url: "https://aplication-gpd4.onrender.com/api/personajesinsertar",
    headers: {
      "Content-Type": "application/json"
    },
    data: json.value
  };

  try {
    const response = await axios.request(options);
    console.log(response.data);
    
    
    json.value = {
      nombre: "",
      edad: "",
      habilidad: "",
      origen: "",
      descripcion: ""
    };

    
    emit("actualizado");
  } catch (error) {
    console.error("Error", error);
  }
};
</script>

<template>
  <div class="container text-center">
    <div class="row">
      <div class="col-4"></div>
      <div class="col-4">
        <form @submit.prevent="boton">
          <div class="row">
            <div v-for="campo in Object.keys(json)" :key="campo" class="col-3">
              <label class="form-label">{{ campo }}</label>
              <input type="text" v-model="json[campo]" class="form-control" />
            </div>
          </div>
          <button type="submit" class="btn btn-primary mt-3">Guardar</button>
        </form>
      </div>
      <div class="col-4"></div>
    </div>
  </div>
</template>
