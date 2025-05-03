<template>
    <div class="card p-3 mt-4">
        <h5 class="text-center">Gráfico de Entradas e Saídas</h5>
        <canvas ref="chartCanvas"></canvas>
        <div class="text-center mt-3">
            <p><strong>Entradas:</strong> R$ {{entradas.reduce((acc, t) => acc + t.amount, 0).toFixed(2)}}</p>
            <p><strong>Saídas:</strong> R$ {{saidas.reduce((acc, t) => acc + Math.abs(t.amount), 0).toFixed(2)}}</p>
            <p><strong>Saldo Total:</strong> R$ {{(entradas.reduce((acc, t) => acc + t.amount, 0) - saidas.reduce((acc,
                t) => acc + Math.abs(t.amount), 0)).toFixed(2) }}</p>
        </div>
        <div class="text-center mt-3">
            <button class="btn btn-primary" @click="renderChart">Atualizar Gráfico</button>
        </div>
    </div>
</template>

<script>
import { Chart, registerables } from 'chart.js';
Chart.register(...registerables);

export default {
    name: 'FinanceChart',
    props: {
    entradas: {
        type: Array,
        default: () => [],
    },
    saidas: {
        type: Array,
        default: () => [],
    }
    },

    data() {
        return {
            chart: null
        };
    },
    watch: {
        entradas: 'renderChart',
        saidas: 'renderChart'
    },
    methods: {
        renderChart() {
            if (!this.entradas.length && !this.saidas.length) return;

            if (this.chart) {
                this.chart.destroy(); // limpa gráfico anterior se existir
            }

            const totalEntradas = (this.entradas || []).reduce((acc, t) => acc + t.amount, 0);
            const totalSaidas = (this.saidas || []).reduce((acc, t) => acc + Math.abs(t.amount), 0);


            const ctx = this.$refs.chartCanvas.getContext('2d');

            this.chart = new Chart(ctx, {
                type: 'pie',
                data: {
                    labels: ['Entradas', 'Saídas'],
                    datasets: [{
                        data: [totalEntradas, totalSaidas],
                        backgroundColor: ['#198754', '#dc3545']
                    }]
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
    },
    mounted() {
        this.renderChart();
    }
};
</script>
