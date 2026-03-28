<template>
  <div class="bg-gray-800 rounded-xl p-4 mb-6">
    <div class="flex items-center gap-2 mb-2">
      <span class="w-2 h-2 bg-green-400 rounded-full"></span>
      <span class="text-xs text-gray-400 font-medium">SQL Generado</span>
    </div>
    <code class="text-green-400 text-sm font-mono">{{ sql }}</code>
  </div>
</template>

<script setup>
defineProps({ sql: String })
</script>