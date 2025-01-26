<template>
  <div id="app">
    <Home />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Home from './views/Home.vue';

export default defineComponent({
  name: 'App',
  components: {
    Home,
  },
});
</script>

<style>
/* Puedes añadir estilos globales aquí si es necesario */
</style>

