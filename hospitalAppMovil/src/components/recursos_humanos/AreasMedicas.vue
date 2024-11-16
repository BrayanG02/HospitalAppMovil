<template>
    <div class="shadow-lg rounded-lg overflow-hidden mx-4 md:mx-10">
      <table class="min-w-full bg-white border border-gray-300">
        <thead>
          <tr class="bg-gray-100 text-gray-600 uppercase text-xs leading-normal">
            <th class="w-1/12 py-4 px-6 text-left">ID</th>
            <th class="w-1/4 py-4 px-6 text-left">Nombre</th>
            <th class="w-1/3 py-4 px-6 text-left">Descripción</th>
            <th class="w-1/6 py-4 px-6 text-left">Estatus</th>
            <th class="w-1/6 py-4 px-6 text-left">Fecha Registro</th>
            <th class="w-1/6 py-4 px-6 text-left">Fecha Actualización</th>
          </tr>
        </thead>
        <tbody class="text-gray-600 text-xs font-light">
          <tr v-for="item in data" :key="item.ID" class="bg-white text-center border-b border-gray-200">
            <td class="py-4 px-6 text-left whitespace-nowrap">{{ item.ID }}</td>
            <td class="py-4 px-6 text-left whitespace-nowrap">{{ item.Nombre }}</td>
            <td class="py-4 px-6 text-left whitespace-nowrap">{{ item.Descripcion }}</td>
            <td class="py-4 px-6 text-left whitespace-nowrap">
              <span :class="{'bg-green-500': item.Estatus === 'Activo', 'bg-red-500': item.Estatus === 'Inactivo'}" class="text-white py-1 px-2 rounded-full text-xs">
                {{ item.Estatus }}
              </span>
            </td>
            <td class="py-4 px-6 text-left whitespace-nowrap">{{ new Date(item.Fecha_Registro).toLocaleDateString() }}</td>
            <td class="py-4 px-6 text-left whitespace-nowrap">{{ new Date(item.Fecha_Actualizacion).toLocaleDateString() }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        data: [],
        token: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJOb21icmVfVXN1YXJpbyI6InJpY2FyZG8iLCJDb3JyZW9fRWxlY3Ryb25pY28iOiJzdHJpbmciLCJDb250cmFzZW5hIjoiMTIzIiwiTnVtZXJvX1RlbGVmb25pY29fTW92aWwiOiJzdHJpbmcifQ.dWVoAwB2f4vq25slE0WlVBldvg4xXL7ixyflkUYCodk'
      };
    },
    mounted() {
      this.fetchData();
    },
    methods: {
      fetchData() {
        axios.get('https://privilegecare-deploy-gqmt.onrender.com/areas_medicas', {
          headers: {
            'Authorization': `Bearer ${this.token}`
          }
        })
        .then(response => {
          this.data = response.data;
          console.log(response.data);
        })
        .catch(error => {
          console.error('Error fetching data:', error);
        });
      }
    }
  }
  </script>
  
  <style scoped>
  /* Añade estilos personalizados si es necesario */
  </style>
  