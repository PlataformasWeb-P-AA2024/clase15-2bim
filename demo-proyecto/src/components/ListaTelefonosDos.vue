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
        <td v-if="t.estudianteDetalle">
            <div>
              <p>Nombre: {{ t.estudianteDetalle.nombre }}</p>
              <p>Apellido: {{ t.estudianteDetalle.apellido }}</p>
              <!-- Agrega más detalles según lo necesites -->
            </div>
          </td>
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
        // Después de obtener los teléfonos, se hace lo adicional
        // para cada nueva llamada
        this.fetchDetalleEstudiante();
      } catch (error) {
        console.error('Error obteniendo telefonos:', error);
      }
    },

    async fetchDetalleEstudiante() {
      const telefonosPromises = this.telefonos.map(async (telefono) => {
        try {
          const response = await axios.get(telefono.estudiante);
          telefono.estudianteDetalle = response.data;
        } catch (error) {
          console.error('Error obteniendo detalles del estudiante:', error);
        }
      });

      // Espera a que todas las solicitudes se completen
      await Promise.all(telefonosPromises);
    }

  }
};
</script>

<style scoped>
/* agregar ---- */
</style>
