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
export default {
  name: "YesNoModal",
  props: {
    Display: {
      default: false
    },

    Header: { default: "You need to set the `Header` prop" },

    Message: { default: "You need to set the `Message` prop" },

    NoBtn: { default: "No" },

    YesBtn: { default: "Yes" },

    NoColor: { default: "red darken-1" },

    YesColor: { default: "green darken-1" }
  },
  methods: {
    CloseResult(res) {
      this.$emit("Result", res);
    }
  }
};
</script>

<style>
</style>

