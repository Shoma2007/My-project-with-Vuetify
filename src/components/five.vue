<template>
 <h1>Пятое задание</h1>
 <p>Время: 40 минут</p>
  <v-container>
    <v-text-field
      v-model="searchQuery"
      label="Поиск пользователей"
      class="mb-4"
    ></v-text-field>
    
    <div v-if="isSearching" class="mb-4">Поиск...</div>

    <div class="mb-4">Найдено: {{ searchResults.length }}</div>

    <div v-if="searchResults.length == 0 && !isSearching">
      Результатов не найдено
    </div>

    <v-list v-else>
      <v-list-item
        v-for="user in searchResults"
        :key="user.id"
      >
        <v-list-item-title>{{ user.name }}</v-list-item-title>
        <v-list-item-subtitle>{{ user.email }}</v-list-item-subtitle>
      </v-list-item>
    </v-list>
  </v-container>
</template>

<script setup>
import { ref, watch } from 'vue'

const users = ref([
  { id: 1, name: "Иван Иванов", email: "ivan@example.com", age: 30 },
  { id: 2, name: "Петр Петров", email: "petr@example.com", age: 25 },
  { id: 3, name: "Мария Сидорова", email: "maria@example.com", age: 28 },
  { id: 4, name: "Алексей Алексеев", email: "alex@example.com", age: 35 },
])

const searchQuery = ref('')
const searchResults = ref([...users.value])
const isSearching = ref(false)

let debounceTimer = null

watch(searchQuery, () => {
  isSearching.value = true
  
  clearTimeout(debounceTimer)
  debounceTimer = setTimeout(() => {
    if (!searchQuery.value.trim()) {
      searchResults.value = [...users.value]
    } else {
      const query = searchQuery.value.toLowerCase()
      searchResults.value = users.value.filter(user => 
        user.name.toLowerCase().includes(query) ||
        user.email.toLowerCase().includes(query)
      )
    }
    isSearching.value = false
  }, 500)
})
</script>
<style scoped>

</style>