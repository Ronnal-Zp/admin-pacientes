<script setup>
  import { ref, reactive } from "vue";
  import { v4 as uuidv4 } from 'uuid';

  import Header from "./components/Header.vue";
  import Formulario from "./components/Formulario.vue";
  import Paciente from "./components/Paciente.vue";

  const pacientes = ref([]);

  const paciente = reactive({
    id: null,
    nombre: '',
    propietario: '',
    email: '',
    alta: '',
    sintomas: ''
  });

  const guardarPaciente = () => {

    if(paciente.id) {
      const { id } =  paciente;
      const index = pacientes.value.findIndex(p => p.id == id);

      if(index > 0) pacientes.value[index] = { ...paciente }

    } else {
      paciente.id = uuidv4();

      console.log('pacienteviejo', paciente);
      console.log('pacientenuevo', {...paciente});
      pacientes.value.push({
        ...paciente
      });
    }

    Object.assign(paciente, {
      nombre: "",
      propietario: "",
      email: "",
      alta: "",
      sintomas: "",
      id: null,
    });
  }

</script>

<template>
  <div class="container mx-auto mt-20">
    <Header />

    <div class="mt-12 md:flex">
      <Formulario 
        v-model:id="paciente.id"
        v-model:nombre="paciente.nombre"
        v-model:propietario="paciente.propietario"
        v-model:email="paciente.email"
        v-model:alta="paciente.alta"
        v-model:sintomas="paciente.sintomas"
        @guardar-paciente="guardarPaciente" 
      />

      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Administra tus pacientes</h3>
        
        <div v-if="pacientes.length > 0">
          <p class="text-lg mt-5 text-center mb-10">
            Informacion de
            <span class="text-indigo-600 font-bold">Pacientes</span> 
          </p>

          <Paciente 
            v-bind:key="paciente.id"
            v-for="paciente in pacientes"
            :paciente="paciente"
          />
        </div>
      
        <p v-else class="mt-10 text-2xl text-center">No hay pascientes</p>
      </div>

    </div>
  </div>
</template>

<style scoped>

</style>
