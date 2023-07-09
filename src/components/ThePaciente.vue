<script setup lang="ts">
import type { IPaciente } from '@/types/Paciente'

defineProps({
  paciente: {
    type: Object as () => IPaciente,
    required: true
  }
})

defineEmits(['editar-paciente', 'eliminar-paciente'])
</script>

<template>
  <div class="my-5 mr-2 bg-white shadow-md px-3 py-4 rounded-md">
    <p class="font-bold mb-3 text-gray-700 text-sm uppercase">
      ID:
      <span class="font-normal normal-case">{{ paciente.id }}</span>
    </p>

    <p class="font-bold mb-3 text-gray-700 text-sm uppercase">
      Nombre:
      <span class="font-normal normal-case">{{ paciente.nombre }}</span>
    </p>

    <p class="font-bold mb-3 text-gray-700 text-sm uppercase">
      Propietario:
      <span class="font-normal normal-case">{{ paciente.propietario }}</span>
    </p>

    <p class="font-bold mb-3 text-gray-700 text-sm uppercase">
      Email:
      <span class="font-normal normal-case">{{ paciente.email }}</span>
    </p>

    <p class="font-bold mb-3 text-gray-700 text-sm uppercase">
      Fecha Alta:
      <span class="font-normal normal-case">{{ paciente.alta }}</span>
    </p>

    <p class="font-bold mb-3 text-gray-700 text-sm uppercase">
      Síntomas:
      <span class="font-normal normal-case">{{ paciente.sintomas }}</span>
    </p>

    <div class="grid md:grid-cols-2 gap-5 mt-5">
      <button
        type="button"
        class="block py-2 px-10 bg-indigo-600 hover:bg-indigo-700 text-white text-sm font-bold uppercase rounded-md"
        @click="$emit('editar-paciente', paciente.id)"
      >
        Editar
      </button>

      <button
        type="button"
        class="block py-2 px-10 bg-red-600 hover:bg-red-700 text-white text-sm font-bold uppercase rounded-md"
        @click="$emit('eliminar-paciente', paciente.id)"
      >
        Eliminar
      </button>
    </div>
  </div>
</template>
