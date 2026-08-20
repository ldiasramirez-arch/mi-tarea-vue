<script setup>
import { ref } from 'vue'

// 1. Variables reactivas para el formulario
const nombre = ref('')
const apellido = ref('')
const genero = ref('')
const carrera = ref('')

// 2. Lista (Array) para guardar todos los registros de estudiantes
const estudiantes = ref([])

// 3. Función que se ejecuta al enviar el formulario
const agregarEstudiante = () => {
  // Creamos un objeto con los datos actuales del formulario
  const nuevoEstudiante = {
    nombre: nombre.value,
    apellido: apellido.value,
    genero: genero.value,
    carrera: carrera.value
  }

  // Agregamos el objeto a nuestra lista de estudiantes
  estudiantes.value.push(nuevoEstudiante)

  // Limpiamos los campos del formulario para el siguiente registro
  nombre.value = ''
  apellido.value = ''
  genero.value = ''
  carrera.value = ''
}
</script>

<template>
  <div class="contenedor">
    <h1>Registro de Estudiantes</h1>

    <!-- FORMULARIO -->
    <form @submit.prevent="agregarEstudiante" class="formulario">
      <div class="campo">
        <label>Nombre:</label>
        <input type="text" v-model="nombre" required />
      </div>

      <div class="campo">
        <label>Apellido:</label>
        <input type="text" v-model="apellido" required />
      </div>

      <div class="campo">
        <label>Género:</label>
        <div class="radios">
          <label><input type="radio" value="Masculino" v-model="genero" required /> Masculino</label>
          <label><input type="radio" value="Femenino" v-model="genero" required /> Femenino</label>
          <label><input type="radio" value="Otro" v-model="genero" required /> Otro</label>
        </div>
      </div>

      <div class="campo">
        <label>Carrera:</label>
        <select v-model="carrera" required>
          <option value="" disabled>Seleccione una carrera</option>
          <option value="Ingeniería en Sistemas">Ingeniería en Sistemas</option>
          <option value="Medicina">Medicina</option>
          <option value="Derecho">Derecho</option>
          <option value="Administración de Empresas">Administración de Empresas</option>
        </select>
      </div>

      <button type="submit">Guardar Registro</button>
    </form>

    <!-- TABLA DE RESULTADOS -->
    <h2>Datos Capturados</h2>
    <table class="tabla">
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Apellido</th>
          <th>Género</th>
          <th>Carrera</th>
        </tr>
      </thead>
      <tbody>
        <!-- Si no hay datos, mostramos un mensaje -->
        <tr v-if="estudiantes.length === 0">
          <td colspan="4" style="text-align: center;">No hay registros ingresados todavía.</td>
        </tr>
        <!-- v-for recorre la lista y dibuja cada fila dinámicamente -->
        <tr v-for="(estudiante, index) in estudiantes" :key="index">
          <td>{{ estudiante.nombre }}</td>
          <td>{{ estudiante.apellido }}</td>
          <td>{{ estudiante.genero }}</td>
          <td>{{ estudiante.carrera }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
