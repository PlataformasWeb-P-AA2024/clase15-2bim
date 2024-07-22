<template>
  <div>
    <h1>Lista de Teléfonos</h1>
    <center>
    <table class="mi-tabla">
      <tr>
        <th>Número</th>
        <th>Tipo</th>
        <th>Estudiante</th>
      </tr>
      <tr v-for="t in telefonos" :key="t.id">
        <td>{{ t.telefono }}</td>
        <td>{{ t.tipo }}</td>
        <td>{{ t.estudiante }}</td>
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
      telefonos: []
    };
  },
  created() {
    this.fetchTelefonos();
  },
  methods: {
    async fetchTelefonos() {
      try {
        const response = await axios.get('http://127.0.0.1:8000/api/numerost/');
        this.telefonos = response.data;
      } catch (error) {
        console.error('Error obteniendo telefonos:', error);
      }
    }
  }
};
</script>

<style scoped>
/* agregar ---- */
</style>
