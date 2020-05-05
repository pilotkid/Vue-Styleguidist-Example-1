<template>
  <v-btn :color="color" @click="$emit('clicked')">
    <slot></slot>
  </v-btn>
</template>

<script>
export default {
  props: {
    color: {
      default: "primary"
    }
  }
};
</script>

<style>
</style>