<template>
<NavBar />


</template>

<script>
import { ref } from 'vue';

import { RouterLink, RouterView } from 'vue-router'
import NavBar from './components/NavBar.vue';

export default {
  name: 'App',
  components: {
    RouterLink,
    RouterView,
    NavBar
  }
};
</script>