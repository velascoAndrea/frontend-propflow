<template>
  <div class="bg-white rounded-xl shadow-sm p-6 mb-6">
    <h2 class="text-lg font-medium text-gray-700 mb-4">
       Busca propiedades en lenguaje natural
    </h2>
    <div class="flex gap-3">
      <input
        v-model="query"
        @keyup.enter="handleSearch"
        type="text"
        placeholder="Ej. Casas con 3 habitaciones en zona 10 menos de Q 200,000"
        class="flex-1 border border-gray-200 rounded-lg px-4 py-3 text-sm focus:outline-none focus:ring-2 focus:ring-blue-500"
        :disabled="loading"
      />
      <button
        @click="handleSearch"
        :disabled="loading || !query.trim()"
        class="bg-blue-600 text-white px-6 py-3 rounded-lg text-sm font-medium hover:bg-blue-700 disabled:opacity-50 disabled:cursor-not-allowed transition-colors"
      >
        {{ loading ? 'Buscando...' : 'Buscar' }}
      </button>
    </div>
    <div class="flex flex-wrap gap-2 mt-3">
      <span class="text-xs text-gray-400">Prueba:</span>
      <button
        v-for="example in examples"
        :key="example"
        @click="query = example"
        class="text-xs text-blue-500 hover:text-blue-700 hover:underline"
      >
        "{{ example }}"
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits(['search'])
const query = ref('')
const props = defineProps({ loading: Boolean })

const examples = [
  'Casas con 3 habitaciones en zona 10',
  'Apartamentos menos de $150,000',
  'Propiedades con más de 2 baños',
  'Terrenos en zona 15'
]

function handleSearch() {
  if (query.value.trim() && !props.loading) {
    emit('search', query.value.trim())
  }
}
</script>