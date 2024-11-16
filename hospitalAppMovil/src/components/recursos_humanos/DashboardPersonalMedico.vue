<template>
  <div style="height: 400px; width: 600px;">
    <h1 class="text-1xl font-bold text-center text-gray-800 my-6">
      Tipos de Personal Médico
    </h1>
    <v-chart :option="chartOptions" style="height: 400px; width: 600px;"></v-chart>
  </div>
</template>

<script>
import { defineComponent, ref, onMounted } from 'vue';
import { use } from 'echarts/core';
import { CanvasRenderer } from 'echarts/renderers';
import { BarChart } from 'echarts/charts';
import { GridComponent, TooltipComponent, LegendComponent } from 'echarts/components';
import VChart from 'vue-echarts';
import axios from 'axios';

use([CanvasRenderer, BarChart, GridComponent, TooltipComponent, LegendComponent]);

export default defineComponent({
  name: 'PersonalMedicoChart',
  components: { VChart },
  setup() {
    const chartOptions = ref(null);
    const token =
  "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJOb21icmVfVXN1YXJpbyI6ImpvbmEyMyIsIkNvcnJlb19FbGVjdHJvbmljbyI6InN0cmluZyIsIkNvbnRyYXNlbmEiOiIxMjM0IiwiTnVtZXJvX1RlbGVmb25pY29fTW92aWwiOiJzdHJpbmcifQ.uGxblZ3LX-pRNbXaGEAs41QWESPwqCIdHmBqokYgPIA";

    const fetchData = async () => {
      const headers = {
        Authorization: `Bearer ${token}`,
      };

      try {
        const response = await axios.get('http://127.0.0.1:8000/personal_medico/', { headers });
        const data = response.data;

        // Contadores por tipo
        const tipoCount = {};

        // Contar tipos de personal
        data.forEach(item => {
          if (tipoCount.hasOwnProperty(item.Tipo)) {
            tipoCount[item.Tipo]++;
          } else {
            tipoCount[item.Tipo] = 1;
          }
        });

        // Convertir datos para gráfico
        const xAxisData = Object.keys(tipoCount);
        const seriesData = xAxisData.map(tipo => tipoCount[tipo]);

        // Configuración del gráfico
        chartOptions.value = {
          tooltip: {
            trigger: 'axis',
            axisPointer: {
              type: 'shadow'
            }
          },
          legend: {
            data: ['Cantidad']
          },
          grid: {
            left: '3%',
            right: '4%',
            bottom: '3%',
            containLabel: true
          },
          xAxis: {
            type: 'category',
            data: xAxisData,
            axisLabel: {
              fontSize: 8,
              lineHeight: 50,
              align: 'center',
              verticalAlign: 'middle',
            }
          },
          yAxis: {
            type: 'value'
          },
          series: [{
            name: 'Cantidad',
            type: 'bar',
            data: seriesData,
            label: {
              show: true,
              position: 'top',
              formatter: '{c}'
            },
            itemStyle: {
              color: '#4CAF50' // Cambia el color según sea necesario
            }
          }]
        };
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    };

    onMounted(() => {
      fetchData();
    });

    return {
      chartOptions,
    };
  },
});
</script>
