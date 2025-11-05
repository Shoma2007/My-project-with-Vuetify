<template>
  <v-container class="d-flex justify-center">
    <v-col cols="12" sm="10" md="8" lg="10">
      <v-card class="pa-6" elevation="2">
        <v-card-title class="text-h4 text-center mb-2"
          >Пятое задание</v-card-title
        >
        <v-card-subtitle class="text-h6 text-center mb-6"
          >Время: 40 минут</v-card-subtitle
        >

        <v-text-field
          v-model="searchQuery"
          label="Поиск пользователей"
          outlined
          clearable
          prepend-inner-icon="mdi-magnify"
          class="mb-4"
        ></v-text-field>

        <v-alert v-if="isSearching" type="info" class="mb-4">
          <v-progress-linear
            indeterminate
            color="white"
            class="mb-2"
          ></v-progress-linear>
          Поиск...
        </v-alert>

        <v-alert
          v-if="!isSearching"
          :type="searchResults.length > 0 ? 'success' : 'warning'"
          class="mb-4"
        >
          <div class="d-flex justify-space-between align-center">
            <span>Найдено пользователей: {{ searchResults.length }}</span>
          </div>
        </v-alert>

        <v-card v-if="searchResults.length > 0" elevation="1">
          <v-list two-line>
            <v-list-item
              v-for="user in searchResults"
              :key="user.id"
              class="mb-2"
            >
              <template v-slot:prepend>
                <v-avatar color="primary" class="mr-4">
                  <span class="white--text text-h6">
                    {{ getUserInitials(user.name) }}
                  </span>
                </v-avatar>
              </template>

              <v-list-item-title class="text-h6 font-weight-medium">
                {{ user.name }}
              </v-list-item-title>

              <v-list-item-subtitle class="text-body-1 mt-1">
                {{ user.email }}
              </v-list-item-subtitle>

              <v-list-item-subtitle class="text-body-2 mt-1">
                Возраст: {{ user.age }} лет
              </v-list-item-subtitle>
            </v-list-item>
          </v-list>
        </v-card>

        <v-alert
          v-else-if="!isSearching && searchQuery"
          type="warning"
          class="text-center mt-4"
        >
          <v-icon large class="mr-2">mdi-account-question</v-icon>
          Пользователи не найдены
        </v-alert>

        <v-alert
          v-else-if="!isSearching && !searchQuery"
          type="info"
          class="text-center mt-4"
        >
          <v-icon large class="mr-2">mdi-account-group</v-icon>
          Введите имя или email для поиска пользователей
        </v-alert>
      </v-card>
    </v-col>
  </v-container>
</template>

<script setup>
import { ref, watch } from "vue";

const users = ref([
  { id: 1, name: "Иван Иванов", email: "ivan@example.com", age: 30 },
  { id: 2, name: "Петр Петров", email: "petr@example.com", age: 25 },
  { id: 3, name: "Мария Сидорова", email: "maria@example.com", age: 28 },
  { id: 4, name: "Алексей Алексеев", email: "alex@example.com", age: 35 },
]);

const searchQuery = ref("");
const searchResults = ref([...users.value]);
const isSearching = ref(false);

let debounceTimer = null;

watch(searchQuery, () => {
  isSearching.value = true;

  clearTimeout(debounceTimer);
  debounceTimer = setTimeout(() => {
    if (!searchQuery.value.trim()) {
      searchResults.value = [...users.value];
    } else {
      const query = searchQuery.value.toLowerCase();
      searchResults.value = users.value.filter(
        (user) =>
          user.name.toLowerCase().includes(query) ||
          user.email.toLowerCase().includes(query)
      );
    }
    isSearching.value = false;
  }, 500);
});

const getUserInitials = (name) => {
  return name
    .split(" ")
    .map((n) => n[0])
    .join("")
    .toUpperCase();
};
</script>
