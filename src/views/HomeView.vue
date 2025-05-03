<template>
  <div class="container py-5">
    <div class="text-center mb-5">
      <h1 class="display-5 fw-bold">💰 Controle de Finanças</h1>
      <p class="text-muted">Gerencie suas entradas e saídas facilmente</p>
    </div>

    <div class="card shadow-sm mb-4">
      <div class="card-body">
        <h5 class="card-title mb-3"><i class="bi bi-plus-circle me-2"></i>Nova Transação</h5>
        <TransactionForm @add-transaction="addTransaction" />
      </div>
    </div>

    <div class="card shadow-sm mb-4">
      <div class="card-body">
        <Summary :transactions="transactions" />
      </div>
    </div>

    <div class="card shadow-sm mb-4">
      <div class="card-body">
        <h5 class="card-title"><i class="bi bi-list-ul me-2"></i>Lista de Transações</h5>
        <TransactionList
          :transactions="transactions"
          @remove-transaction="removeTransaction"
        />
      </div>
    </div>

    <div class="card shadow-sm mb-4">
      <div class="card-body">
        <h5 class="card-title"><i class="bi bi-bar-chart-line me-2"></i>Gráfico Financeiro</h5>
        <FinanceChart :entradas="entradas" :saidas="saidas" />
      </div>
    </div>

    <RouterView />
  </div>
</template>


<script>
import { RouterLink, RouterView } from 'vue-router'
 import FinanceChart from '../components/FinanceChart.vue';
import TransactionForm from '../components/TransactionForm.vue';
import TransactionList from '../components/TransactionList.vue';
import Summary from '../components/Summary.vue';


export default {
  components: {
  
    RouterLink,
    TransactionForm,
    TransactionList,
    Summary,
    FinanceChart
    
  },
  data() {
    return {
      transactions: []
    };
  },
  computed: {
    entradas() {
      return this.transactions.filter(t => t.type === 'entrada');
    },
    saidas() {
      return this.transactions.filter(t => t.type === 'saida');
    },
    saldoTotal() {
      return this.transactions.reduce((acc, t) => acc + t.amount, 0);
    }
  },
  methods: {
    addTransaction(transaction) {
      this.transactions.push(transaction);
      this.saveTransactions();
    },
    removeTransaction(index) {
      this.transactions.splice(index, 1);
      this.saveTransactions();
    },
    saveTransactions() {
      localStorage.setItem('transactions', JSON.stringify(this.transactions));
    },
    loadTransactions() {
      const stored = localStorage.getItem('transactions');
      if (stored) {
        this.transactions = JSON.parse(stored);
      }
    }
  },
  mounted() {
    this.loadTransactions();
  }
};
</script>
