<template>
  <v-container class="d-flex justify-center">
    <v-col cols="12" sm="8" md="6" lg="10">
      <v-card class="pa-6 text-center" elevation="2">
        <v-card-title class="text-h4 mb-4">Первое задание</v-card-title>
        <v-card-subtitle class="text-h6 mb-4">Время: 7 минут</v-card-subtitle>

        <v-card-text>
          <p class="text-h3 mb-6 primary--text">{{ counter }}</p>

          <v-row class="justify-center">
            <v-col cols="12" sm="4">
              <v-btn @click="increment()" color="primary" block large>
                Увеличить
              </v-btn>
            </v-col>
            <v-col cols="12" sm="4">
              <v-btn @click="decrement()" color="secondary" block large>
                Уменьшить
              </v-btn>
            </v-col>
            <v-col cols="12" sm="4">
              <v-btn @click="resetTo()" color="error" block large>
                Сбросить
              </v-btn>
            </v-col>
          </v-row>
        </v-card-text>
      </v-card>
    </v-col>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      counter: 0,
    };
  },
  methods: {
    increment() {
      this.counter++;
    },
    decrement() {
      this.counter--;
    },
    resetTo() {
      this.counter = 0;
    },
  },
};
</script>
