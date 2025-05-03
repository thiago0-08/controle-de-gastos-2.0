<template>
  

  <div class="container py-5">
    <h1 class="text-center mb-4">Controle de Finanças</h1>
    <TransactionForm @add-transaction="addTransaction" />
    <Summary :transactions="transactions" class="mb-4" />
    <TransactionList :transactions="transactions" @remove-transaction="removeTransaction" />

    <FinanceChart :entradas="entradas" :saidas="saidas" />
    
  </div>
  <RouterView />
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
