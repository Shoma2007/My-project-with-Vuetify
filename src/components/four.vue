<template>
 <h1>Четвертое задание</h1>
 <p>Время: 25 минут</p>
 <v-text-field  type="text" v-model="name" class="inp" label="Введите имя:"/>
 <p class="error" v-if="name.length <= 1">{{ error_name }}</p>
 <v-text-field type="email" v-model="email" class="inp" label="Введите email:"/>
 <p class="error" v-if="!email.includes('@gmail') && !email.includes('@mail')">{{ error_email }}</p>
 <v-text-field type="password" v-model="password" class="inp" label="Введите пароль:"/>
 <p class="error" v-if="password.length <= 5">{{ error_password }}</p>
 <v-btn @click="registr()">Зарегистрироваться</v-btn>
</template>

<script setup>
import { ref } from "vue";

const name = ref('')
const email = ref('')
const password = ref('')
const error_name = ref('')
const error_email = ref('')
const error_password = ref('')

const registr = () => {
    if(name.value.length <= 1){
        error_name.value = 'Должно быть минимум 2 символа'
        return
    } else if (!email.value.includes("@gmail") && !email.value.includes("@mail")) {
    error_email.value = "Email должен содержать символ @ и иметь почту (mail, gmail)";
    return;
  } else if (password.value.length <= 5){
    error_password.value = "Пароль должен иметь минимум 6 символов";
    return;
  } else {
    alert('Вы успешно зарегистрировались')
  }
  name.value = ''
  email.value = ''
  password.value = ''
  error_name.value = ''
  error_email.value = ''
  error_password.value = ''
}
</script>

<style scoped>
.error{
    color:red
}
.inp{
    width: 300px;
}
</style>
