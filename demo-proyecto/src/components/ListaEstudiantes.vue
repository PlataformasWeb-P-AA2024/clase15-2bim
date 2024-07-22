<template>
  <div>
    <h1>Lista de Estudiantes</h1>
    <center>
    <table class="mi-tabla">
      <tr>
        <th>Nombre</th>
        <th>Apellido</th>
      </tr>
      <tr v-for="estudiante in estudiantes" :key="estudiante.id">
        <td>{{ estudiante.nombre }}</td>
        <td>{{ estudiante.apellido }}</td>
      </tr>
    </table>
    </center>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      estudiantes: []
    };
  },
  created() {
    this.fetchEstudiantes();
  },
  methods: {
    async fetchEstudiantes() {
      try {
        const response = await axios.get('http://127.0.0.1:8000/api/estudiantes/');
        this.estudiantes = response.data;
      } catch (error) {
        console.error('Error obteniendo estudiantes:', error);
      }
    }
  }
};
</script>

<style scoped>
/* agregar ---- */
</style>
