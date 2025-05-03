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
        console.error("Erro ao calcular totais:", error);
        return 0;
      }
    }
  }
}
</script>

<template>
  <div>
   
    <FinanceChart :entradas="entradas" :saidas="saidas" />
  </div>
</template>