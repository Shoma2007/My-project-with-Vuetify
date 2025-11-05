<template>
  <v-container class="d-flex justify-center">
    <v-col cols="12" sm="8" md="6" lg="10">
      <v-card class="pa-6" elevation="2">
        <v-card-title class="text-h4 text-center mb-2"
          >Четвертое задание</v-card-title
        >
        <v-card-subtitle class="text-h6 text-center mb-6"
          >Время: 25 минут</v-card-subtitle
        >

        <v-form @submit.prevent="registr()">
          <v-text-field
            type="text"
            v-model="name"
            label="Введите имя:"
            outlined
            class="mb-2"
            :error-messages="name.length <= 1 ? error_name : ''"
          />

          <v-text-field
            type="email"
            v-model="email"
            label="Введите email:"
            outlined
            class="mb-2"
            :error-messages="
              !email.includes('@gmail') && !email.includes('@mail') && email
                ? error_email
                : ''
            "
          />

          <v-text-field
            type="password"
            v-model="password"
            label="Введите пароль:"
            outlined
            class="mb-4"
            :error-messages="
              password.length <= 5 && password ? error_password : ''
            "
          />

          <v-btn type="submit" color="primary" block large class="mt-4">
            Зарегистрироваться
          </v-btn>
        </v-form>
      </v-card>
    </v-col>
  </v-container>
</template>

<script setup>
import { ref } from "vue";

const name = ref("");
const email = ref("");
const password = ref("");
const error_name = ref("Должно быть минимум 2 символа");
const error_email = ref(
  "Email должен содержать символ @ и иметь почту (mail, gmail)"
);
const error_password = ref("Пароль должен иметь минимум 6 символов");

const registr = () => {
  if (name.value.length <= 1) {
    return;
  } else if (
    !email.value.includes("@gmail") &&
    !email.value.includes("@mail")
  ) {
    return;
  } else if (password.value.length <= 5) {
    return;
  } else {
    alert("Вы успешно зарегистрировались");
  }
  name.value = "";
  email.value = "";
  password.value = "";
};
</script>
