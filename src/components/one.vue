<template>
  <h1>Первая задания</h1>
  <p>Время: 7 минут</p>
  <p>Считчик: {{ counter }}</p>
  <v-btn @click="increment()">Увеличить</v-btn>
  <v-btn @click="decrement()">Уменьшить</v-btn>
  <v-btn @click="resetTo()">Сбросить</v-btn>
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

<style scoped>

</style>
