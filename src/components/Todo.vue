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

        <!-- <v-btn v-if="detailFlag" color="primary" @click="addTodo" dense>
          save
        </v-btn> -->

        <v-btn v-if="detailFlag" color="primary" @click="addTodo" small>
          save
        </v-btn>
      </div>

      <v-tabs v-model="currentItem" fixed-tabs slider-color="white">
        <v-tab v-for="item in items" :key="item" :href="`#${item}`">
          {{ item }}
        </v-tab>
      </v-tabs>

      <v-tabs-items v-model="currentItem">
        <v-tab-item v-for="item in items" :key="item" :value="item">
          <!-- todo area -->
          <v-list v-if="filterTodos.length">
            <v-list-item
              dense
              v-for="(todo, index) in filterTodos"
              :key="todo.id"
              class="pr-0"
              height="50"
            >
              <!-- chk box -->
              <v-list-item-action>
                <v-checkbox v-model="todo.done" color="primary" />
              </v-list-item-action>

              <!-- todo -->
              <v-list-item-content @click="showDialog($refs.dialogRef[index])">
                <v-list-item-title
                  :class="{ done: todo.done }"
                  v-text="todo.title"
                />
                <v-list-item-subtitle v-text="todo.detail" />
                <!-- show dialog -->
                <todo-dialog :todo="todo" ref="dialogRef" />
              </v-list-item-content>

              <!-- del btn-->
              <v-list-item-action>
                <v-btn outlined @click="delTodo(index)">del</v-btn>
              </v-list-item-action>
            </v-list-item>
          </v-list>

          <div v-else>
            <h3>no item</h3>
          </div>
        </v-tab-item>
      </v-tabs-items>
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
      currentItem: "active",
      items: ["active", "done"],
      edit: {},
      title: "",
      detail: "",
      todos: [],
      detailFlag: false
    };
  },
  computed: {
    filterTodos() {
      let flg = this.currentItem === "done";
      return this.todos.filter(todo => todo.done === flg);
    }
  },
  methods: {
    addTodo() {
      if (this.title) {
        this.todos.push({
          title: this.title,
          detail: this.detail,
          done: false,
          edit: false,
          id: this.todos.length
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
