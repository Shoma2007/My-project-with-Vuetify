<template>
  <h1>Второе задание</h1>
  <p>Время: 20 минут</p>
  <v-text-field type="text" v-model="task" class="inp" label="Добавьте задачу:"/>
  <v-btn @click="sendData()">Добавть задачу</v-btn>
  <p class="error">{{ error }}</p>
  <h2>TODO-LIST</h2>
  <v-container v-for="(el, index) in tasks" :key="index" class="conteiner">
    <p>{{ el.tas }}</p>
    <v-btn @click="deleteUsers(index)" class="error">Удалить</v-btn>
  </v-container>
  
</template>

<script>
export default {
  data() {
    return {
      tasks: [],
      error: "",
      task: "",
    };
  },
  methods: {
    sendData() {
      if (this.task.length > 0) {
        this.tasks.push({
          tas: this.task,
        });
      } else {
        this.error = "Заполните задачу";
        return;
      }
      this.error = "";
      this.task = "";
    },
    deleteUsers(index) {
    this.tasks.splice(index, 1);
    }
  },
};
</script>

<style scoped>
.error{
  color: red;
}
.conteiner{
  display: flex;
  justify-content: space-between;
  background-color: gray;
  margin-top: 10px;
}
.inp{
  width: 500px;
}
</style>
