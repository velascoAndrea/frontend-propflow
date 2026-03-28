<template>
  <div>
    <!-- Loading -->
    <div v-if="loading" class="flex flex-col items-center py-16 text-gray-400">
      <div class="w-8 h-8 border-2 border-blue-500 border-t-transparent rounded-full animate-spin mb-3"></div>
      <span class="text-sm">Analizando tu consulta...</span>
    </div>

    <!-- Error -->
    <div v-else-if="error" class="bg-red-50 border border-red-200 rounded-xl p-4 text-red-600 text-sm">
      {{ error }}
    </div>

    <!-- No results -->
    <div v-else-if="searched && results.length === 0" class="text-center py-16 text-gray-400">
      <span class="text-4xl block mb-3">🏠</span>
      <p class="text-sm">No se encontraron propiedades para tu búsqueda</p>
    </div>

    <!-- Results -->
    <div v-else-if="results.length > 0">
      <p class="text-sm text-gray-500 mb-4">{{ results.length }} Propiedades encontradas</p>
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
        <PropertyCard v-for="prop in results" :key="prop.id" :property="prop" />
      </div>
    </div>
  </div>
</template>

<script setup>
import PropertyCard from './PropertyCard.vue'
defineProps({
  results: Array,
  loading: Boolean,
  error: String,
  searched: Boolean
})
</script>