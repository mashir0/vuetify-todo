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
      <!-- title -->
      <v-text-field
        outlined
        label="Title"
        v-model="title"
        @keyup.enter="addTodo"
        @keyup.esc="title = ''"
        clearable
      />

      <!-- detail -->
      <v-textarea
        v-if="detailFlag"
        label="Detail"
        auto-grow
        rows="1"
        row-height="15"
        v-model="detail"
        class="pt-0 mr-2 ml-2"
      />

      <!-- btn area -->
      <div class="d-flex">
        <v-btn @click="detailFlag = !detailFlag" icon class="mr-2">
          <v-icon dark>mdi-playlist-plus</v-icon>
        </v-btn>
        <v-btn icon class="mr-2 mr-auto">
          <v-icon dark>mdi-calendar-clock</v-icon>
        </v-btn>

        <v-btn v-if="detailFlag" color="primary" @click="addTodo">
          save
        </v-btn>
      </div>

      <!-- todo area -->
      <v-list v-if="todos.length">
        <v-list-item
          dense
          v-for="(todo, index) in todos"
          :key="index"
          class="pl-0"
        >
          <!-- chk box -->
          <v-list-item-action>
            <v-checkbox v-model="todo.done" color="primary"></v-checkbox>
          </v-list-item-action>

          <!-- todo -->
          <v-list-item-content @click="showDialog($refs.dialogRef[index])">
            <v-list-item-title
              :class="{ done: todo.done }"
              v-text="todo.title"
            />
            <!-- show dialog -->
            <todo-dialog :todo="todo" ref="dialogRef" />
          </v-list-item-content>

          <!-- del btn-->
          <v-list-item-action>
            <v-row>
              <v-btn outlined @click="delTodo(index)">del</v-btn>
            </v-row>
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
import TodoDialog from "@/components/TodoDialog";

export default {
  name: "HelloWorld",

  components: {
    TodoDialog
  },
  data() {
    return {
      edit: {},
      title: "",
      detail: "",
      todos: [],
      detailFlag: false
    };
  },
  methods: {
    addTodo() {
      if (this.title) {
        this.todos.push({
          title: this.title,
          detail: this.detail,
          done: false,
          edit: false
        });
        this.title = "";
        this.detail = "";
      }
    },

    delTodo(index) {
      this.todos.splice(index, 1);
    },

    showDialog(_refs) {
      // console.log(_refs);
      _refs.toggle();
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
