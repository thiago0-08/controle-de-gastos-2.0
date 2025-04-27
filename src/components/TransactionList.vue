<template>
    <div class="card p-3">
      <h3 class="mb-3">Transações</h3>
      <ul class="list-group">
        <li v-for="(transaction, index) in transactions" :key="index" class="list-group-item d-flex justify-content-between align-items-center">
          <div>
            <strong>{{ transaction.name }}</strong><br />
            <small>{{ formatDate(transaction.date) }} - {{ transaction.type === 'entrada' ? 'Entrada' : 'Saída' }}</small>
          </div>
          <div class="d-flex align-items-center">
            <span :class="transaction.amount > 0 ? 'text-success' : 'text-danger'">
              {{ formatCurrency(transaction.amount) }}
            </span>
            <button @click="$emit('remove-transaction', index)" class="btn btn-sm btn-outline-danger ms-3">Remover</button>
          </div>
        </li>
      </ul>
    </div>
  </template>
  
  
  
  <script>
  export default {
    props: {
      transactions: Array
    },
    methods: {
      formatCurrency(value) {
        return Number(value).toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
      },
      formatDate(date) {
        const [year, month, day] = date.split('-');
        return `${day}/${month}/${year}`;
      }
    }
  };
  </script>
  
  <style scoped>
  .transactions li {
    margin-top: 10px;
    list-style: none;
  }
  </style>
  