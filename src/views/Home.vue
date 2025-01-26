<template>
  <div>
    <RegistroEstacionamiento />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import RegistroEstacionamiento from '../components/RegistroEstacionamiento.vue';

export default defineComponent({
  name: 'Home',
  components: {
    RegistroEstacionamiento,
  },
});
</script>

<style>
/* Puedes añadir estilos globales aquí si es necesario */
</style>

