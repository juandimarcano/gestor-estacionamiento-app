<template>
  <div class="container">
    <h1 class="text-center my-4">Registro de Estacionamiento</h1>
    <form @submit.prevent="guardarRegistro">
      <div class="mb-3">
        <label class="form-label">Nombre</label>
        <input v-model="registro.nombre" type="text" class="form-control" />
      </div>
      <div class="mb-3">
        <label class="form-label">Documento de Identidad</label>
        <input v-model="registro.documento" type="number" class="form-control" />
      </div>
      <div class="mb-3">
        <label class="form-label">Teléfono</label>
        <input v-model="registro.telefono" type="number" class="form-control" />
      </div>
      <div class="mb-3">
        <label class="form-label">Placa del Carro</label>
        <input v-model="registro.placa" type="text" class="form-control" />
      </div>
      <div class="mb-3">
        <label class="form-label">Lugar de Estacionamiento</label>
        <input v-model="registro.lugar" type="number" class="form-control" />
      </div>
      <div class="mb-3">
        <label class="form-label">Monto \$</label>
        <input v-model="registro.monto" type="number" class="form-control" />
      </div>
      <button type="submit" class="btn btn-primary">Guardar Registro</button>
    </form>

    <h2 class="text-center my-4">Registros</h2>
    <table class="table table-striped">
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Documento</th>
          <th>Teléfono</th>
          <th>Placa</th>
          <th>Lugar</th>
          <th>Monto \$</th>
          <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(registro, index) in registros" :key="index">
          <td>{{ registro.nombre }}</td>
          <td>{{ registro.documento }}</td>
          <td>{{ registro.telefono }}</td>
          <td>{{ registro.placa }}</td>
          <td>{{ registro.lugar }}</td>
          <td>{{ registro.monto }}</td>
          <td>
            <button @click="eliminarRegistro(index)" class="btn btn-danger">Eliminar</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script lang="ts">
import { defineComponent, reactive, onMounted } from 'vue';

interface Registro {
  nombre: string;
  documento: string;
  telefono: string;
  placa: string;
  lugar: string;
  monto: number;
}

export default defineComponent({
  name: 'RegistroEstacionamiento',
  setup() {
    const registro = reactive<Registro>({
      nombre: '',
      documento: '',
      telefono: '',
      placa: '',
      lugar: '',
      monto: 0,
    });

    const registros = reactive<Registro[]>([]);

    const guardarRegistro = () => {
      const lugarOcupado = registros.some(reg => reg.lugar === registro.lugar);
      if (lugarOcupado) {
        alert('El lugar de estacionamiento ya está ocupado.');
        return;
      }
      registros.push({ ...registro });
      actualizarLocalStorage();
      limpiarFormulario();
    };

    const eliminarRegistro = (index: number) => {
      registros.splice(index, 1);
      actualizarLocalStorage();
    };

    const actualizarLocalStorage = () => {
      localStorage.setItem('registros', JSON.stringify(registros));
    };

    const cargarRegistros = () => {
    const registrosGuardados = localStorage.getItem('registros');
      if (registrosGuardados) {
        Object.assign(registros, JSON.parse(registrosGuardados));
      }
    };

    const limpiarFormulario = () => {
      registro.nombre = '';
      registro.documento = '';
      registro.telefono = '';
      registro.placa = '';
      registro.lugar = '';
      registro.monto = 0;
    };

    onMounted(() => {
      cargarRegistros();
    });

    return {
      registro,
      registros,
      guardarRegistro,
      eliminarRegistro,
    };
  },
});
</script>
