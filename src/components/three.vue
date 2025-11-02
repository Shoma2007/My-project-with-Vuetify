<template>
 <h1>Третье задание</h1>
 <p>Время: 28 минут</p>
 <v-container>
 <v-select 
 label="Фильтр по категории" 
 v-model="Selcategory" 
 :items="categories" 
 class="mb-4" 
 style="width: 300px;"/>
 <v-row>
 <v-col
 v-for="product in filterProducts" 
 :key="product.id"
 cols="12"
 md="4"
 sm="6"
 >
 <v-alert> 
  Найдено товаров: {{ filterProducts.length }}
 </v-alert>
 <v-card class="pa-4" >
 <v-card-title>
    {{ product.name }}
 </v-card-title>
 <v-card-subtitle>
    {{ product.category }}
 </v-card-subtitle>
 <v-card-text>
    {{ product.price }}
 </v-card-text>
 </v-card>
</v-col>
 </v-row>
 </v-container>
</template>

<script setup>
import { ref, computed} from "vue";

const products = ref([
    {id: 1, naem: 'Ноутбук', price: 50000, category: 'Электроника'},
    {id: 2, naem: 'Футболка', price: 1500, category: 'Одежда'},
    {id: 3, naem: 'Книга Vue.js', price: 800, category: 'Книга'},
    {id: 4, naem: 'Смартфон', price: 30000, category: 'Электроника'},
    {id: 5, naem: 'Джинсы', price: 2500, category: 'Одежда'},
    {id: 6, naem: 'Книга JavaScript', price: 950, category: 'Книга'}
])

const Selcategory = ref('Все категории')

const categories = computed(() => [
    'Все категории',
    ...new Set(products.value.map(p => p.category))
])

const filterProducts = computed(() => {
    if (Selcategory.value == 'Все категории') {
        return products.value
    }
    return products.value.filter(product => 
        product.category == Selcategory.value
    )
})
</script>

<style scoped>
</style>
