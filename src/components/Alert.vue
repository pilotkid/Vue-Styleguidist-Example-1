<template>
  <v-row justify="center">
    <v-dialog v-model="Display" persistent max-width="500">
      <v-card>
        <v-card-title class="headline">{{Header}}</v-card-title>
        <v-card-text>{{Message}}</v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <!-- 
            This is the close event, that notifies the parent that the modal should be closed 
            @event Close
          -->
          <v-btn :color="BtnColor" depressed dark @click="$emit('Close')">{{CloseText}}</v-btn>
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

    /**
     * The header message that displays above the body message
     * @values any string
     */
    Header: { default: "You need to set the `Header` prop" },

    /**
     * This is the main body message
     */
    Message: { default: "You need to set the `Message` prop" },

    /**
     * This is the text to go on the close button
     */
    CloseText: { default: "Okay" },

    /**
     * This is the color of the close button
     * @values primary, secondary, accent, error, info, success, warning
     */
    BtnColor: { default: "primary" }
  }
};
</script>

<style>
</style>
