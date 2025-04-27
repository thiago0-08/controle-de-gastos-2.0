<template>
    <form @submit.prevent="handleSubmit" class="card p-3 mb-4">
      <div class="mb-3">
        <label class="form-label">Nome</label>
        <input v-model="transaction.name" type="text" class="form-control" placeholder="Nome" required />
      </div>
  
      <div class="mb-3">
        <label class="form-label">Valor</label>
        <input v-model.number="transaction.amount" type="number" class="form-control" placeholder="Valor" required />
      </div>
  
      <div class="mb-3">
        <label class="form-label">Data</label>
        <input v-model="transaction.date" type="date" class="form-control" required />
      </div>
  
      <div class="mb-3">
        <label class="form-label">Tipo</label>
        <select v-model="transaction.type" class="form-select" required>
          <option value="">Selecione</option>
          <option value="entrada">Entrada</option>
          <option value="saida">Saída</option>
        </select>
      </div>
  
      <button type="submit" class="btn btn-primary w-100">Adicionar</button>
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
  