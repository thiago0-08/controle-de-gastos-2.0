<template>
    <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
      <div class="container">
        <router-link class="navbar-brand" to="/">Meu App</router-link>
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
              <router-link class="nav-link" active-class="active" to="/">Home</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" active-class="active" to="/about">Sobre</router-link>
            </li>
            <li class="nav-item dropdown">
              <a
                class="nav-link dropdown-toggle"
                href="#"
                role="button"
                data-bs-toggle="dropdown"
                aria-expanded="false"
              >
                Dropdown
              </a>
              <ul class="dropdown-menu">
                <li><router-link class="dropdown-item" to="/item1">Item 1</router-link></li>
                <li><router-link class="dropdown-item" to="/item2">Item 2</router-link></li>
                <li><hr class="dropdown-divider" /></li>
                <li><router-link class="dropdown-item" to="/item3">Item 3</router-link></li>
              </ul>
            </li>
          </ul>
          <form class="d-flex" role="search">
            <input class="form-control me-2" type="search" placeholder="Pesquisar" aria-label="Search" />
            <button class="btn btn-outline-light" type="submit">Buscar</button>
          </form>
        </div>
      </div>
    </nav>
  </template>
  
  <script>
  import { ref } from 'vue';
  
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
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
  
  .nav-link.router-link-exact-active {
    font-weight: bold;
  }
  </style>