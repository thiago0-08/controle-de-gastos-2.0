<template>
  <div class="card shadow-sm p-3 mb-4">
    <h5 class="mb-3"><i class="bi bi-list-ul me-2"></i>Transações</h5>

    <ul class="list-group list-group-flush">
      <li
        v-for="(transaction, index) in transactions"
        :key="index"
        class="list-group-item d-flex justify-content-between align-items-center"
      >
        <div>
          <strong>{{ transaction.name }}</strong><br />
          <small class="text-muted">
            <i
              :class="transaction.type === 'entrada' ? 'bi bi-arrow-down-circle text-success' : 'bi bi-arrow-up-circle text-danger'"
              class="me-1"
            ></i>
            {{ formatDate(transaction.date) }} – {{ transaction.type === 'entrada' ? 'Entrada' : 'Saída' }}
          </small>
        </div>

        <div class="d-flex align-items-center">
          <span
            class="badge fs-6"
            :class="transaction.amount > 0 ? 'bg-success' : 'bg-danger'"
          >
            {{ formatCurrency(transaction.amount) }}
          </span>
          <button
            @click="$emit('remove-transaction', index)"
            class="btn btn-sm btn-outline-danger ms-3"
            title="Remover transação"
          >
            <i class="bi bi-trash"></i>
          </button>
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
  