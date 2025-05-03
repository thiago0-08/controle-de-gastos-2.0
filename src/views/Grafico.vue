<script setup>
import FinanceChart from '../components/FinanceChart.vue';

defineProps({
  entradas: Array,
  saidas: Array
});
</script>

<template>
  <FinanceChart :entradas="entradas" :saidas="saidas" />
</template>

