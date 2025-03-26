<script setup>
    import { reactive } from "vue";
    import Alerta from "./Alerta.vue";

    const alerta = reactive({
        tipo: '',
        mensaje: ''
    });

    const paciente = reactive({
        nombre: '',
        propietario: '',
        email: '',
        alta: '',
        sintomas: ''
    });


    const validar = () => {

        if (Object.values(paciente).includes('')) {
            alerta.mensaje = 'Todos los campos son obligatorios';
            alerta.tipo = 'error';
            return;
        }

        console.log('Validar..')
        alerta.mensaje = 'Guardado correctamente';
        alerta.tipo = 'exito';

    }

</script>

<template>
    <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center">Seguimiento Pacientes</h2>
        
        <p class="text-lg mt-5 text-center mb-10">
            Añade Pacientes y 
            <span class="text-indigo-600 font-bold">Administradores</span>
        </p>

        <Alerta
            v-if="alerta.mensaje"
            :alerta="alerta"
        />

        <form   
            @submit.prevent="validar"
            class="bg-white shadow-md rounded-lg py-10 px-5 mb-10">
            <div class="mb-5">
                <label 
                    for="mascota" 
                    class="block text-gray-700 uppercase font-bold">
                    Nombre mascota
                </label>
                <input 
                    v-model="paciente.nombre"
                    id="mascota" 
                    class="border-2 border-gray-400 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    placeholder="Nombre de la mascota" 
                    type="text">
            </div>

            <div class="mb-5">
                <label 
                    for="propietario" 
                    class="block text-gray-700 uppercase font-bold">
                    Nombre Propietario
                </label>
                <input 
                    v-model="paciente.propietario"
                    id="propietario" 
                    class="border-2 border-gray-400 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    placeholder="Nombre de propietario" 
                    type="text">
            </div>

            <div class="mb-5">
                <label 
                    for="email" 
                    class="block text-gray-700 uppercase font-bold">
                    Email
                </label>
                <input 
                    v-model="paciente.email"
                    id="email" 
                    class="border-2 border-gray-400 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    placeholder="Email de propietario" 
                    type="email">
            </div>

            <div class="mb-5">
                <label 
                    for="alta" 
                    class="block text-gray-700 uppercase font-bold">
                    Alta
                </label>
                <input 
                    v-model="paciente.alta"
                    id="alta" 
                    class="border-2 border-gray-400 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    type="date">
            </div>

            <div class="mb-5">
                <label 
                    for="sintomas" 
                    class="block text-gray-700 uppercase font-bold">
                    Sintomas
                </label>
                <textarea
                    v-model="paciente.sintomas" 
                    id="sintomas" 
                    class="border-2 border-gray-400 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    placeholder="Escribe los sintomas" />
            </div>

            <input class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors" type="submit" value="Registrar paciente">
        </form>
    </div>
</template>
