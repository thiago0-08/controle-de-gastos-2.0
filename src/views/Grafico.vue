<script>
import FinanceChart from '../components/FinanceChart.vue';

export default {
  components: {
    FinanceChart
  },
  props: {
    entradas: {
      type: Array,
      default: () => []
    },
    saidas: {
      type: Array,
      default: () => []
    }
  },
  computed: {
    totalEntradas() {
      try {
        return this.entradas?.reduce((acc, curr) => acc + curr.value, 0) || 0;
      } catch (error) {
        console.error("Erro ao calcular total de entradas:", error);
        return 0;
      }
    },
    totalSaidas() {
      try {
        return this.saidas?.reduce((acc, curr) => acc + curr.value, 0) || 0;
      } catch (error) {
        console.error("Erro ao calcular total de saídas:", error);
        return 0;
      }
    }
  }
}
</script>

<template>
  <div class="container mt-4">
    <h1>Gráfico de Entradas e Saídas</h1>
    <div class="row">
      <div class="col-md-6">
        <FinanceChart :entradas="entradas" :saidas="saidas" />
      </div>
      <div class="col-md-6">
        <h2>Resumo Financeiro</h2>  
        <p><strong>Entradas:</strong> R$ {{ totalEntradas.toFixed(2) }}</p>
        <p><strong>Saídas:</strong> R$ {{ totalSaidas.toFixed(2) }}</p>
        <p><strong>Saldo Total:</strong> R$ {{ (totalEntradas - totalSaidas).toFixed(2) }}</p>
      </div>
    </div>
  </div>
</template>

