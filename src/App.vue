<script setup lang="ts">
import { onMounted, reactive, ref, watch } from 'vue'
import { uid } from 'uid'
import TheHeader from '@/components/TheHeader.vue'
import TheFormulario from '@/components/TheFormulario.vue'
import ThePaciente from '@/components/ThePaciente.vue'
import type { IPaciente } from './types/Paciente'

const pacientes = ref<IPaciente[]>([])
const paciente = reactive({
  id: null,
  nombre: '',
  propietario: '',
  email: '',
  alta: '',
  sintomas: ''
})

watch(pacientes, () => guardarLS(), { deep: true })

const guardarLS = () => localStorage.setItem('pacientes', JSON.stringify(pacientes.value))

onMounted(() => {
  const pacientesLS = localStorage.getItem('pacientes')
  if (pacientesLS) pacientes.value = JSON.parse(pacientesLS)
})

const guardarPaciente = () => {
  if (paciente.id) {
    const { id } = paciente
    const index = pacientes.value.findIndex((paciente) => paciente.id === id)
    pacientes.value[index] = { ...paciente }
  } else {
    pacientes.value.push({ ...paciente, id: uid() })
  }
  Object.assign(paciente, {
    id: null,
    nombre: '',
    propietario: '',
    email: '',
    alta: '',
    sintomas: ''
  })
}

const editarPaciente = (id: string) => {
  const pacienteEditar = pacientes.value.filter((paciente) => paciente.id === id)[0]
  Object.assign(paciente, pacienteEditar)
}

const eliminarPaciente = (id: string) => {
  pacientes.value = pacientes.value.filter((paciente) => paciente.id !== id)
}
</script>

<template>
  <div class="container mx-auto mt-20">
    <TheHeader />
    <div class="mt-16 md:flex md:gap-5">
      <TheFormulario
        v-model:nombre="paciente.nombre"
        v-model:propietario="paciente.propietario"
        v-model:email="paciente.email"
        v-model:alta="paciente.alta"
        v-model:sintomas="paciente.sintomas"
        @guardar-paciente="guardarPaciente"
        :id="paciente.id"
      />
      <div class="md:w-1/2 h-screen overflow-y-scroll">
        <h3 class="text-2xl text-center text-gray-800 font-bold">Administra tus pacientes</h3>
        <div v-if="pacientes.length > 0">
          <p class="my-2 text-gray-700 text-center font-semibold">
            Información de
            <span class="text-indigo-600">pacientes</span>
          </p>
          <ThePaciente
            v-for="paciente in pacientes"
            :key="paciente.id"
            :paciente="paciente"
            @editar-paciente="editarPaciente"
            @eliminar-paciente="eliminarPaciente"
          />
        </div>
        <p v-else class="mt-2 text-center text-gray-700 font-bold">No hay pacientes</p>
      </div>
    </div>
  </div>
</template>
