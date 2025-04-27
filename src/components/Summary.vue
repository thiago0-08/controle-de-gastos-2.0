<template>
    <div class="row text-center">
      <div class="col-md-4 mb-3">
        <div class="card p-3 bg-success text-white">
          <h5>Entradas</h5>
          <p>R$ {{ income }}</p>
        </div>
      </div>
      <div class="col-md-4 mb-3">
        <div class="card p-3 bg-danger text-white">
          <h5>Saídas</h5>
          <p>R$ {{ expense }}</p>
        </div>
      </div>
      <div class="col-md-4 mb-3">
        <div class="card p-3 bg-primary text-white">
          <h5>Total</h5>
          <p>R$ {{ total }}</p>
        </div>
      </div>
    </div>
  </template>
  
  
  <script>
  export default {
    props: {
      transactions: Array
    },
    computed: {
      income() {
        return this.transactions
          .filter(t => t.amount > 0)
          .reduce((sum, t) => sum + t.amount, 0)
          .toFixed(2);
      },
      expense() {
        return this.transactions
          .filter(t => t.amount < 0)
          .reduce((sum, t) => sum + t.amount, 0)
          .toFixed(2);
      },
      total() {
        return (parseFloat(this.income) + parseFloat(this.expense)).toFixed(2);
      }
    }
  };
  </script>
  
  <style scoped>
  .summary p {
    margin: 5px 0;
  }
  </style>
  