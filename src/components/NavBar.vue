<template>
    <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
      <div class="container">
        <RouterLink class="navbar-brand" to="/">Meu App</RouterLink>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
          @click="toggleNav"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" :class="{ show: isNavOpen }" id="navbarNav">
          <ul class="navbar-nav me-auto">
            <li class="nav-item">
              <RouterLink class="nav-link" active-class="active" to="/">Home</RouterLink>
            </li>
            <li class="nav-item">
              <RouterLink class="nav-link" active-class="active" to="/about">Sobre</RouterLink>
            </li>
            <li class="nav-item">
              <RouterLink class="nav-link" active-class="active" to="/grafico">Gráfico</RouterLink>
            </li>
            
          </ul>
          <form class="d-flex" role="search">
            <input class="form-control me-2" type="search" placeholder="Pesquisar" aria-label="Search" />
            <button class="btn btn-outline-light" type="submit">Buscar</button>
          </form>
        </div>
      </div>
    </nav>
    <RouterView />
  </template>
  
  <script>
  import { ref } from 'vue';
  import { RouterLink, RouterView } from 'vue-router'
  
  export default {
    name: 'NavbarComponent',
    setup() {
      const isNavOpen = ref(false);
  
      const toggleNav = () => {
        isNavOpen.value = !isNavOpen.value;
      };
  
      return {
        isNavOpen,
        toggleNav,
      };
    },
  };
  </script>
  
  <style scoped>
  .navbar {
    box-shadow: 0 2px 4px rgba(255, 255, 255, 0.1);
  }
  
  .nav-link.RouterLink-exact-active {
    font-weight: bold;
  }
  </style>