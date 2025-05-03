<template>
  <div class="card shadow-sm p-4 mt-4">
    <h5 class="text-center mb-4">
      <i class="bi bi-bar-chart-fill me-2 text-primary"></i>Gráfico de Entradas e Saídas
    </h5>

    <canvas ref="chartCanvas"></canvas>

    <div class="row text-center mt-4">
      <div class="col-md-4 mb-2">
        <div class="text-success fw-semibold">
          <i class="bi bi-arrow-down-circle me-1"></i>
          Entradas
        </div>
        <span class="badge bg-success fs-6">
          R$ {{ entradas.reduce((acc, t) => acc + t.amount, 0).toFixed(2) }}
        </span>
      </div>
      <div class="col-md-4 mb-2">
        <div class="text-danger fw-semibold">
          <i class="bi bi-arrow-up-circle me-1"></i>
          Saídas
        </div>
        <span class="badge bg-danger fs-6">
          R$ {{ saidas.reduce((acc, t) => acc + Math.abs(t.amount), 0).toFixed(2) }}
        </span>
      </div>
      <div class="col-md-4 mb-2">
        <div class="text-dark fw-semibold">
          <i class="bi bi-wallet2 me-1"></i>
          Saldo Total
        </div>
        <span
          class="badge fs-6"
          :class="saldoTotal >= 0 ? 'bg-primary' : 'bg-secondary'"
        >
          R$ {{ saldoTotal.toFixed(2) }}
        </span>
      </div>
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
  computed: {
    saldoTotal() {
      const totalEntradas = this.entradas.reduce((acc, t) => acc + t.amount, 0);
      const totalSaidas = this.saidas.reduce((acc, t) => acc + Math.abs(t.amount), 0);
      return totalEntradas - totalSaidas;
    }
  },
  mounted() {
    const ctx = this.$refs.chartCanvas.getContext('2d');

    const totalEntradas = this.entradas.reduce((acc, t) => acc + t.amount, 0);
    const totalSaidas = this.saidas.reduce((acc, t) => acc + Math.abs(t.amount), 0);

    new Chart(ctx, {
      type: 'bar',
      data: {
        labels: ['Entradas', 'Saídas'],
        datasets: [
          {
            label: 'R$',
            data: [totalEntradas, totalSaidas],
            backgroundColor: ['#198754', '#dc3545'],
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
  max-width: 100%;
  margin: auto;
  display: block;
}
</style>
