<template>
  <div class="bg-white rounded-xl shadow-sm p-5 hover:shadow-md transition-shadow">
    <div class="flex justify-between items-start mb-3">
      <span class="text-xs font-medium px-2 py-1 rounded-full"
        :class="{
          'bg-blue-100 text-blue-700': property.tipo === 'casa',
          'bg-purple-100 text-purple-700': property.tipo === 'departamento',
          'bg-green-100 text-green-700': property.tipo === 'terreno',
          'bg-orange-100 text-orange-700': property.tipo === 'oficina'
        }">
        {{ property.tipo }}
      </span>
      <span class="text-lg font-bold text-blue-600">
        $ {{ formatPrice(property.precio) }}
      </span>
    </div>

    <h3 class="font-medium text-gray-800 mb-1 text-sm">{{ property.titulo }}</h3>
    <p class="text-xs text-gray-500 mb-3 line-clamp-2">{{ property.descripcion }}</p>

    <div class="flex items-center gap-3 text-xs text-gray-500 mb-2">
      <span v-if="property.habitaciones > 0">🛏 {{ property.habitaciones }} habs</span>
      <span v-if="property.banos > 0">🚿 {{ property.banos }} baños</span>
      <span v-if="property.area_m2 > 0">📐 {{ property.area_m2 }}m²</span>
    </div>

    <div class="flex items-center gap-1 text-xs text-gray-400">
      <span>📍</span>
      <span>{{ property.ubicacion }}</span>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({ property: Object })

function formatPrice(price) {
  return Number(price).toLocaleString('en-US')
}
</script>