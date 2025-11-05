<template>
  <v-container class="d-flex justify-center">
    <v-col cols="12" sm="10" md="8" lg="10">
      <v-card class="pa-6" elevation="2">
        <v-card-title class="text-h4 text-center mb-2"
          >Второе задание</v-card-title
        >
        <v-card-subtitle class="text-h6 text-center mb-6"
          >Время: 20 минут</v-card-subtitle
        >

        <v-row class="align-end mb-4">
          <v-col cols="12" sm="8">
            <v-text-field
              type="text"
              v-model="task"
              label="Добавьте задачу:"
              outlined
              clearable
              @keypress.enter="sendData()"
            />
          </v-col>
          <v-col cols="12" sm="5">
            <v-btn @click="sendData()" color="primary" block large>
              Добавить задачу
            </v-btn>
          </v-col>
        </v-row>

        <v-alert v-if="error" type="error" class="mb-4">
          {{ error }}
        </v-alert>

        <v-card v-if="tasks.length > 0" class="mt-4">
          <v-card-title class="text-h5 text-center primary white--text">
            TODO-LIST
          </v-card-title>
          <v-list>
            <v-list-item v-for="(el, index) in tasks" :key="index" class="mb-2">
              <v-list-item-content>
                <v-list-item-title class="text-h6">
                  {{ el.tas }}
                </v-list-item-title>
              </v-list-item-content>
              <v-list-item-action>
                <v-btn @click="deleteUsers(index)" color="error" icon>
                  Х
                </v-btn>
              </v-list-item-action>
            </v-list-item>
          </v-list>
        </v-card>
      </v-card>
    </v-col>
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
      if (this.task && this.task.length > 0) {
        this.tasks.push({
          tas: this.task,
        });
        this.error = "";
        this.task = "";
      } else {
        this.error = "Заполните задачу";
      }
    },
    deleteUsers(index) {
      this.tasks.splice(index, 1);
    },
  },
};
</script>

<style scoped></style>
