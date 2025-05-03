<template>
  <div class="row text-center">
    <div class="col-md-4 mb-3">
      <div class="card p-3 bg-success text-white shadow-sm">
        <h6>
          <i class="bi bi-arrow-down-circle me-2"></i>Entradas
        </h6>
        <span class="badge bg-light text-success fs-5">
          R$ {{ income }}
        </span>
      </div>
    </div>
    <div class="col-md-4 mb-3">
      <div class="card p-3 bg-danger text-white shadow-sm">
        <h6>
          <i class="bi bi-arrow-up-circle me-2"></i>Saídas
        </h6>
        <span class="badge bg-light text-danger fs-5">
          R$ -{{ Math.abs(expense) }}
        </span>
      </div>
    </div>
    <div class="col-md-4 mb-3">
      <div class="card p-3 bg-primary text-white shadow-sm">
        <h6>
          <i class="bi bi-wallet2 me-2"></i>Total
        </h6>
        <span class="badge bg-light text-primary fs-5">
          R$ {{ total }}
        </span>
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
  
  