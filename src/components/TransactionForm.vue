<template>
  <form @submit.prevent="handleSubmit" class="card p-4 shadow-sm mb-4">
    <h5 class="mb-3"><i class="bi bi-pencil-square me-2"></i>Nova Transação</h5>

    <!-- Nome -->
    <div class="mb-3">
      <label class="form-label fw-semibold">Nome</label>
      <div class="input-group">
        <span class="input-group-text"><i class="bi bi-tag"></i></span>
        <input v-model="transaction.name" type="text" class="form-control" placeholder="Ex: Salário, Compra" required />
      </div>
    </div>

    <!-- Valor -->
    <div class="mb-3">
      <label class="form-label fw-semibold">Valor</label>
      <div class="input-group">
        <span class="input-group-text"><i class="bi bi-currency-dollar"></i></span>
        <input v-model.number="transaction.amount" type="number" class="form-control" placeholder="0.00" required />
      </div>
    </div>

    <!-- Data -->
    <div class="mb-3">
      <label class="form-label fw-semibold">Data</label>
      <div class="input-group">
        <span class="input-group-text"><i class="bi bi-calendar-date"></i></span>
        <input v-model="transaction.date" type="date" class="form-control" required />
      </div>
    </div>

    <!-- Tipo -->
    <div class="mb-4">
      <label class="form-label fw-semibold">Tipo</label>
      <div class="input-group">
        <span class="input-group-text"><i class="bi bi-arrow-left-right"></i></span>
        <select v-model="transaction.type" class="form-select" required>
          <option value="">Selecione</option>
          <option value="entrada">Entrada</option>
          <option value="saida">Saída</option>
        </select>
      </div>
    </div>

    <!-- Botão -->
    <button type="submit" class="btn btn-success w-100">
      <i class="bi bi-plus-circle me-2"></i>Adicionar Transação
    </button>
  </form>
</template>

  
  <script>
  export default {
    data() {
      return {
        transaction: {
          name: '',
          amount: null,
          date: '',
          type: '' // entrada ou saída
        }
      };
    },
    methods: {
      handleSubmit() {
        // Corrige o valor dependendo do tipo
        let amount = this.transaction.amount;
        if (this.transaction.type === 'saida' && amount > 0) {
          amount *= -1; // Se for saída, valor negativo
        }
  
        this.$emit('add-transaction', { 
          name: this.transaction.name,
          amount: amount,
          date: this.transaction.date,
          type: this.transaction.type
        });
  
        this.transaction.name = '';
        this.transaction.amount = null;
        this.transaction.date = '';
        this.transaction.type = '';
      }
    }
  };
  </script>
  
  
  <style scoped>
  form input, form button {
    display: block;
    margin-bottom: 10px;
    width: 100%;
  }
  </style>
  