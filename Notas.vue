<template>
  <div class="contenedor">
    <h1>Notas</h1>

    <div class="campo">
      <label>Materia</label>
      <input v-model="materia" type="text" placeholder="Ingrese la materia">
    </div>

    <div class="campo">
      <label>Fecha</label>
      <input v-model="fecha" type="date">
    </div>

    <div class="campo">
      <label>Nota</label>
      <input v-model="nota" type="number" placeholder="Ingrese la nota">
    </div>

    <button class="btn" @click="agregar">Agregar</button>

    <p v-if="error" class="error">{{ error }}</p>

    <div v-if="resultado" class="resultado">
      <p>Materia: {{ resultado.materia }}</p>
      <p>Fecha: {{ resultado.fecha }}</p>
      <p>Nota: {{ resultado.nota }}</p>
      <span v-if="resultado.nota >= 7" class="aprobado">Aprobado</span>
      <span v-else class="desaprobado">Desaprobado</span>
    </div>

  </div>
</template>

<script setup>
import { ref } from 'vue'

const materia = ref("")
const fecha = ref("")
const nota = ref("")
const error = ref("")
const resultado = ref(null)



function agregar() {
  if (materia.value == "" || fecha.value == "" || nota.value == "") {
    error.value = "Completá todos los campos."
    return
  }

  if (nota.value < 1 || nota.value > 10) {
    error.value = "La nota debe ser un número entre 1 y 10."
    return
  }

  error.value = ""
  resultado.value = { materia: materia.value, fecha: fecha.value, nota: Number(nota.value) }
  materia.value = ""
  fecha.value = ""
  nota.value = ""
}
</script>

<style scoped>
.contenedor {
  width: 320px;
  padding: 70px;
  margin: 50px auto;
  background-color: #1e1b4b;
  border: 1px solid #4338ca;
  border-radius: 12px;
  color: #e0e7ff;
}

.contenedor h1 {
  margin-top: 0;
  color: #c7d2fe;
}

.campo {
  display: flex;
  flex-direction: column;
  margin-bottom: 12px;
}

.campo label {
  margin-bottom: 4px;
  color: #a5b4fc;
}

.campo input {
  padding: 8px;
  background-color: #312e81;
  border: 1px solid #6366f1;
  color: #e0e7ff;
}

.btn {
  width: 100%;
  padding: 10px;
  background-color: #6366f1;
  color: white;
  border: 1px solid #818cf8;
  cursor: pointer;
  margin-top: 4px;
}

.btn:hover {
  background-color: #4f46e5;
}

.resultado {
  margin-top: 16px;
  padding: 10px;
  border: 1px solid #4f46e5;
  background-color: #272462;
}

.resultado p {
  margin: 0 0 6px 0;
  color: #e0e7ff;
}

.aprobado {
  color: green;
}

.desaprobado {
  color: red;
}

.error {
  color: red;
}
</style>