<template>
  <v-container class="d-flex justify-center">
    <v-col cols="12" lg="10">
      <v-card class="pa-6" elevation="2">
        <v-card-title class="text-h4 text-center mb-2"
          >Третье задание</v-card-title
        >
        <v-card-subtitle class="text-h6 text-center mb-6"
          >Время: 28 минут</v-card-subtitle
        >

        <v-row class="align-center mb-6">
          <v-col cols="12" md="6">
            <v-select
              label="Фильтр по категории"
              v-model="Selcategory"
              :items="categories"
              outlined
              clearable
            />
          </v-col>
          <v-col cols="12" md="6">
            <v-alert type="info" class="mb-0">
              <div class="text-h6">
                Найдено товаров: {{ filterProducts.length }}
              </div>
            </v-alert>
          </v-col>
        </v-row>

        <v-row v-if="filterProducts.length > 0">
          <v-col
            v-for="product in filterProducts"
            :key="product.id"
            cols="12"
            sm="6"
            md="4"
            lg="3"
          >
            <v-card class="pa-4 h-100" elevation="4" hover>
              <v-card-title class="text-h6 text-truncate">
                {{ product.name }}
              </v-card-title>

              <v-card-subtitle class="mb-2">
                <v-chip
                  small
                  :color="getCategoryColor(product.category)"
                  class="white--text"
                >
                  {{ product.category }}
                </v-chip>
              </v-card-subtitle>

              <v-card-text class="text-h5 primary--text font-weight-bold">
                {{ formatPrice(product.price) }} ₽
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>

        <v-alert v-else type="warning" class="text-center mt-6">
          <v-icon large class="mr-2">mdi-magnify</v-icon>
          Товары по выбранной категории не найдены
        </v-alert>
      </v-card>
    </v-col>
  </v-container>
</template>

<script setup>
import { ref, computed } from "vue";

const products = ref([
  { id: 1, name: "Ноутбук", price: 50000, category: "Электроника" },
  { id: 2, name: "Футболка", price: 1500, category: "Одежда" },
  { id: 3, name: "Книга Vue.js", price: 800, category: "Книга" },
  { id: 4, name: "Смартфон", price: 30000, category: "Электроника" },
  { id: 5, name: "Джинсы", price: 2500, category: "Одежда" },
  { id: 6, name: "Книга JavaScript", price: 950, category: "Книга" },
]);

const Selcategory = ref("Все категории");

const categories = computed(() => [
  "Все категории",
  ...new Set(products.value.map((p) => p.category)),
]);

const filterProducts = computed(() => {
  if (Selcategory.value === "Все категории" || !Selcategory.value) {
    return products.value;
  }
  return products.value.filter(
    (product) => product.category === Selcategory.value
  );
});

const formatPrice = (price) => {
  return new Intl.NumberFormat("ru-RU").format(price);
};

const getCategoryColor = (category) => {
  const colors = {
    Электроника: "blue",
    Одежда: "green",
    Книга: "orange",
  };
  return colors[category] || "grey";
};
</script>

<style scoped>
.h-100 {
  height: 100%;
}
</style>
