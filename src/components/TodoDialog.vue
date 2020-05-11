<template>
  <v-row justify="center">
    <v-dialog v-model="dialog" persistent max-width="290">
      <!-- <template v-slot:activator="{ on }">
        <v-btn color="primary" dark v-on="on">show</v-btn>
      </template> -->
      <slot v-bind:dialog="dialog" />

      <v-card>
        <v-card-title class="headline">{{ todo.title }}</v-card-title>
        <v-card-text class="return">{{ todo.detail }}</v-card-text>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="green darken-1" text @click="dialog = false"
            >close</v-btn
          >
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
export default {
  name: "TodoDialog",
  props: {
    todo: Object
  },

  data() {
    return {
      dialog: false
    };
  },

  methods: {
    toggle() {
      // console.log(this.dialog);
      this.dialog = !this.dialog;
    }
  }
};
</script>

<style scoped>
.return {
  white-space: pre-wrap;
  word-wrap: break-word;
}
</style>
