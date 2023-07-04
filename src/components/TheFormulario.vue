<script setup lang="ts">
import { reactive } from 'vue'
import TheAlert from '@/components/TheAlert.vue'
import { type IPaciente } from '@/types/Paciente'

const alerta = reactive({
  tipo: '',
  mensaje: ''
})

const paciente = reactive<IPaciente>({
  nombre: '',
  propietario: '',
  email: '',
  alta: '',
  sintomas: ''
})

const validar = () => {
  if (Object.values(paciente).includes('')) {
    alerta.mensaje = 'Todos los campos son obligatorios'
    alerta.tipo = 'error'
    return
  }
  
}

</script>

<template>
  <div class="md:w-1/2">
    <h2 class="text-gray-800 text-2xl text-center font-bold">Seguimiento paciente</h2>
    <p class="my-2 text-gray-700 text-center font-semibold">
      Añade paciente y
      <span class="text-indigo-600">adminístralo</span>
    </p>
    <TheAlert v-if="alerta.mensaje" :alerta="alerta"/>
    <form class="bg-gray-100 shadow-md rounded-md py-10 px-5 my-5" @submit.prevent="validar">
      <div class="mb-5">
        <label for="mascota" class="block text-gray-700 text-sm uppercase font-bold">
          Nombre Mascota
        </label>
        <input
          id="mascota"
          class="border-2 border-gray-400 w-full py-1 px-2 mt-2 placeholder-gray-500 rounded-md placeholder:text-sm focus:outline-none focus:border-indigo-600 focus:ring-indigo-600"
          type="text"
          placeholder="Nombre de la mascota"
          v-model="paciente.nombre"
        />
      </div>
      <div class="mb-5">
        <label for="mascota" class="block text-gray-700 text-sm uppercase font-bold">
          Nombre Propietario
        </label>
        <input
          id="propietario"
          class="border-2 border-gray-400 w-full py-1 px-2 mt-2 placeholder-gray-500 rounded-md placeholder:text-sm focus:outline-none focus:border-indigo-600 focus:ring-indigo-600"
          type="text"
          placeholder="Nombre del propietario"
          v-model="paciente.propietario"
        />
      </div>
      <div class="mb-5">
        <label for="email" class="block text-gray-700 text-sm uppercase font-bold">Email</label>
        <input
          id="email"
          class="border-2 border-gray-400 w-full py-1 px-2 mt-2 placeholder-gray-500 rounded-md placeholder:text-sm focus:outline-none focus:border-indigo-600 focus:ring-indigo-600"
          type="email"
          placeholder="Email del propietario"
          v-model="paciente.email"
        />
      </div>
      <div class="mb-5">
        <label for="alta" class="block text-gray-700 text-sm uppercase font-bold">Alta</label>
        <input
          id="alta"
          class="border-2 border-gray-400 w-full py-1 px-2 mt-2 placeholder-gray-500 rounded-md placeholder:text-sm focus:outline-none focus:border-indigo-600 focus:ring-indigo-600"
          type="date"
          v-model="paciente.alta"
        />
      </div>
      <div class="mb-5">
        <label for="sintomas" class="block text-gray-700 text-sm uppercase font-bold">
          Síntomas
        </label>
        <textarea
          id="propietario"
          class="h-24 border-2 border-gray-400 w-full py-1 px-2 mt-2 placeholder-gray-500 rounded-md placeholder:text-sm focus:outline-none focus:border-indigo-600 focus:ring-indigo-600"
          placeholder="Describe los síntomas"
          v-model="paciente.sintomas"
        />
      </div>
      <input
        class="bg-indigo-600 text-white text-sm text-center font-bold uppercase py-3 rounded-md w-full cursor-pointer transition-colors duration-500 hover:bg-indigo-700"
        type="submit"
        value="Agregar paciente"
      />
    </form>
  </div>
</template>
