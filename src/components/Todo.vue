<template>
  <!-- <v-content> -->
  <v-container>
    <v-card class="mx-auto mb-5" outlined shaped max-width="500">
      <v-card-title>Vuetify 学習</v-card-title>
      <v-card-text>
        TodoアプリをVuetifyで作り変え
      </v-card-text>
    </v-card>

    <v-card class="mx-auto mb-5 pa-5" outlined shaped max-width="500">
      <h1>todos</h1>
      <v-text-field
        outlined
        label="title"
        v-model="title"
        @keyup.enter="addTodo"
        @keyup.esc="title = ''"
        clearable
      >
      </v-text-field>

      <v-list v-if="todos.length">
        <v-list-item dense v-for="(todo, index) in todos" :key="index">
          <!-- chk box -->
          <v-list-item-action>
            <v-checkbox v-model="todo.done" color="primary"></v-checkbox>
          </v-list-item-action>

          <!-- todo -->
          <v-list-item-content>
            <v-list-item-title
              :class="{ done: todo.done }"
              v-text="todo.title"
            />
          </v-list-item-content>

          <!-- del btn-->
          <v-list-item-action>
            <v-btn outlined @click="delTodo(index)">del</v-btn>
          </v-list-item-action>
        </v-list-item>
      </v-list>

      <div v-else>
        <h3>todoがありません</h3>
      </div>
    </v-card>
  </v-container>
  <!-- </v-content> -->
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      edit: {},
      title: "",
      todos: []
    };
  },
  methods: {
    addTodo() {
      if (this.title) {
        this.todos.push({
          title: this.title,
          done: false,
          edit: false
        });
        this.title = "";
        this.content = "";
      }
    },

    delTodo(index) {
      this.todos.splice(index, 1);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.done {
  text-decoration: line-through;
}
</style>
