<template>
  <div class="min-h-screen bg-gray-50">
    <header class="bg-white shadow-sm">
      <div class="max-w-5xl mx-auto px-4 py-4 flex items-center gap-3">
        <div class="w-8 h-8 bg-blue-600 rounded-lg flex items-center justify-center">
          <span style="color:white;font-weight:bold;font-size:14px">P</span>
        </div>
        <h1 class="text-xl font-semibold text-gray-800">PropFlow</h1>
        <span class="text-sm text-gray-400">Búsqueda de Propiedades</span>
      </div>
    </header>

    <main class="max-w-5xl mx-auto px-4 py-8">
      <SearchBar @search="handleSearch" :loading="loading" />
      <SQLDisplay v-if="sqlQuery" :sql="sqlQuery" />
      <ResultsPanel
        :results="results"
        :loading="loading"
        :error="error"
        :searched="searched"
      />
    </main>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'
import SearchBar from './components/SearchBar.vue'
import SQLDisplay from './components/SQLDisplay.vue'
import ResultsPanel from './components/ResultsPanel.vue'

const results = ref([])
const sqlQuery = ref('')
const loading = ref(false)
const error = ref('')
const searched = ref(false)

async function handleSearch(query) {
  loading.value = true
  error.value = ''
  sqlQuery.value = ''
  searched.value = true

  try {
    const response = await axios.post('http://localhost:8000/api/search', {
      query: query
    })
    results.value = response.data.resultados
    sqlQuery.value = response.data.sql_generado
  } catch (err) {
    error.value = err.response?.data?.detail || 'Error connecting to server'
    results.value = []
  } finally {
    loading.value = false
  }
}
</script>