<template>
  <v-row justify="center">
    <v-dialog v-model="Display" persistent max-width="500">
      <v-card>
        <v-card-title class="headline">{{Header}}</v-card-title>
        <v-card-text>{{Message}}</v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn :color="BtnColor" depressed dark @click="CloseResult()">{{CloseText}}</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
export default {
  name: "AlertModal",

  props: {
    Display: {
      default: false
    },
    Header: { default: "You need to set the `Header` prop" },
    Message: { default: "You need to set the `Message` prop" },

    CloseText: { default: "Okay" },
    BtnColor: { default: "primary" }
  },
  methods: {
    CloseResult() {
      this.$emit("Close");
    }
  }
};
</script>

<style>
</style>
