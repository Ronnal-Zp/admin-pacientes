<script setup>
    import { reactive } from "vue";
    import Alerta from "./Alerta.vue";

    const props = defineProps({
        id: {
            type: [String, null],
            required: true
        },
        nombre: {
            type: String,
            required: true
        },
        propietario: {
            type: String,
            required: true
        },
        email: {
            type: String,
            required: true
        },
        alta: {
            type: String,
            required: true
        },     
        sintomas: {
            type: String,
            required: true
        }     
    })

    const alerta = reactive({
        tipo: '',
        mensaje: ''
    });


    const emit = defineEmits([
        'update:nombre',
        'update:propietario',
        'update:email',
        'update:alta',
        'update:sintomas',
        'guardar-paciente'
    ]);

    const validar = () => {

        if (Object.values(props).includes('')) {
            alerta.mensaje = 'Todos los campos son obligatorios';
            alerta.tipo = 'error';
            return;
        }

        alerta.mensaje = 'Guardado correctamente';
        alerta.tipo = 'exito';      
        emit('guardar-paciente');


        setTimeout(()=> {
            Object.assign(alerta, {
                mensaje: '',
                tipo: ''
            })
        }, 1500)
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
                    @input="$emit('update:nombre', $event.target.value)"
                    :value="nombre"
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
                    @input="$emit('update:propietario', $event.target.value)"
                    :value="propietario"
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
                    @input="$emit('update:email', $event.target.value)"
                    :value="email"
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
                    @input="$emit('update:alta', $event.target.value)"
                    :value="alta"
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
                    @input="$emit('update:sintomas', $event.target.value)"
                    :value="sintomas"
                    id="sintomas" 
                    class="border-2 border-gray-400 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    placeholder="Escribe los sintomas" />
            </div>

            <input class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors" type="submit" value="Registrar paciente">
        </form>
    </div>
</template>
