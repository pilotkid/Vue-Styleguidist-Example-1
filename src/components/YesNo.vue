<template>
  <v-row justify="center">
    <v-dialog v-model="Display" persistent max-width="500">
      <v-card>
        <v-card-title class="headline">{{Header}}</v-card-title>
        <v-card-text>{{Message}}</v-card-text>
        <v-card-actions>
          <v-btn :color="NoColor" depressed dark @click="CloseResult(false)">{{NoBtn}}</v-btn>
          <v-spacer></v-spacer>
          <v-btn :color="YesColor" depressed dark @click="CloseResult(true)">{{YesBtn}}</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
/**
 * This is a yes no dialog component that allows you to ask the user a yes no question
 */
export default {
  name: "YesNoModal",
  props: {
    /**
     * This controls if the modal is visible or not
     * @values true, false
     */
    Display: {
      default: false
    },

    /**
     * Popup header giving a breif description
     * @values any string
     */
    Header: { default: "You need to set the `Header` prop" },

    /**
     * Message content, typically a paragraph
     * @values any string
     */
    Message: { default: "You need to set the `Message` prop" },

    /**
     * This is the No button text
     * @values any string
     */
    NoBtn: { default: "No" },

    /**
     * This is the Yes button text
     * @values any string
     */
    YesBtn: { default: "Yes" },

    /**
     * This is the color of the No button
     * @values primary, secondary, accent, error, info, success, warning
     */
    NoColor: { default: "red darken-1" },

    /**
     * this is the color of the yes button
     * @values primary, secondary, accent, error, info, success, warning
     */
    YesColor: { default: "green darken-1" }
  },
  methods: {
    CloseResult(res) {
      this.Display = false;
      /**
       * The result of the dialog, `false` for no, and `true` for yes
       *
       * @event Result
       * @property {boolean} res The result of the dialog, `false` for no, and `true` for yes
       */
      this.$emit("Result", res);
    }
  }
};
</script>


<style>
</style>

