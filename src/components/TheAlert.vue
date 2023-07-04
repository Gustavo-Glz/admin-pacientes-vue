<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps({
  alerta: {
    type: Object,
    required: true
  }
})

const isError = computed(() => {
  return props.alerta.tipo === 'error'
})
</script>

<template>
  <div
    class="text-white text-sm text-center font-bold uppercase py-3 mb-3 rounded-md"
    :class="[isError ? 'bg-red-500' : 'bg-green-500']"
  >
    {{ alerta.mensaje }}
  </div>
</template>
