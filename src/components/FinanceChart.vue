<template>
    <div class="card p-3 mt-4">
      <h5 class="text-center">Gráfico de Entradas e Saídas</h5>
      <canvas ref="chartCanvas"></canvas>
        <div class="text-center mt-3">
            <p><strong>Entradas:</strong> R$ {{ entradas.reduce((acc, t) => acc + t.amount, 0).toFixed(2) }}</p>
            <p><strong>Saídas:</strong> R$ {{ saidas.reduce((acc, t) => acc + Math.abs(t.amount), 0).toFixed(2) }}</p>
            <p><strong>Saldo Total:</strong> R$ {{ (entradas.reduce((acc, t) => acc + t.amount, 0) + saidas.reduce((acc, t) => acc + Math.abs(t.amount), 0)).toFixed(2) }}</p>
        </div>

      
    </div>
  </template>
  
  <script>
  import { Chart, registerables } from 'chart.js';
  
  Chart.register(...registerables);
  
  export default {
    name: 'FinanceChart',
    props: {
      entradas: Array,
      saidas: Array
    },
    mounted() {
      const ctx = this.$refs.chartCanvas.getContext('2d');
  
      const totalEntradas = this.entradas.reduce((acc, t) => acc + t.amount, 0);
      const totalSaidas = this.saidas.reduce((acc, t) => acc + Math.abs(t.amount), 0); // tira o sinal negativo
  
      new Chart(ctx, {
        type: 'bar',
        data: {
          labels: ['Entradas', 'Saídas'],
          datasets: [
            {
              label: 'R$',
              data: [totalEntradas, totalSaidas],
              backgroundColor: ['#198754', '#dc3545'], // verde e vermelho
              borderColor: ['#146c43', '#b02a37'],
              borderWidth: 1
            }
          ]
        },
        options: {
          responsive: true,
          plugins: {
            legend: {
              position: 'bottom'
            }
          }
        }
      });
    }
  };
  </script>
  

<style scoped>
  canvas {
    max-width: 800px;
    margin: auto;
  }
</style>