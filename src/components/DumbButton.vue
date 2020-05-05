<template>
  <!-- 
  This event is emitted whenever the button is clicked
  @event clicked 
  -->
  <v-btn :color="color" @click="$emit('clicked')">
    <!-- @slot This is the button contents -->
    <slot></slot>
  </v-btn>
</template>

<script>
export default {
  props: {
    /**
     * This is the color of the close button
     * @values primary, secondary, accent, error, info, success, warning
     */
    color: {
      default: "primary"
    }
  }
};
</script>

<style>
</style>