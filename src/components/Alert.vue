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
/**
 * This provides a quick alert to the user, that they must confirm before continuing
 */
export default {
  name: "AlertModal",

  props: {
    /**
     * This controls if the modal is present on the screen
     * @values true, false
     */
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
      /**
       * This is fired when the ok button is pressed
       */
      this.$emit("Close");
    }
  }
};
</script>

<style>
</style>
