<!-- src/components/Sobre.vue -->
<template>
  <div class="sobre">
    <h1>Controle de Gastos 2.0</h1>
    <p>
      Este projeto é uma aplicação web desenvolvida com Vue 3 e Vite, com o objetivo de ajudar os usuários a gerenciar suas finanças pessoais.
    </p>
    <h2>Funcionalidades</h2>
    <ul>
      <li>Cadastro de receitas e despesas</li>
      <li>Visualização de saldo atual</li>
      <li>Listagem de transações</li>
      <li>Organização por categorias</li>
    </ul>
    <h2>Tecnologias Utilizadas</h2>
    <ul>
      <li>Vue 3</li>
      <li>Vite</li>
      <li>JavaScript</li>
    </ul>
    <h2>GitHub </h2>
    
    <p>
      Para mais informações, acesse o repositório no GitHub:
      <a href="https://github.com/thiago0-08/controle-de-gastos-2.0" target="_blank">controle-de-gastos-2.0</a>
    </p>
  </div>
</template>

<script>
export default {
  name: 'Sobre',
};
</script>

<style scoped>
.sobre {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}
</style>
