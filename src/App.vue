<template>
  <v-app>
    <v-app-bar app color="secondary" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />
      </div>
      <h1>Styleguidist - Tutorial 1 (Installation)</h1>
    </v-app-bar>

    <v-content class="ma-3">
      <v-container fill-height>
        <v-row justify="center">
          <v-col cols="6" align="start">
            <DumbButton align="center" @clicked="ShowAlert=!ShowAlert">Fire Alert Modal</DumbButton>
          </v-col>
          <v-col cols="6" align="end">
            <DumbButton color="warning" @clicked="ShowYesNo=!ShowYesNo">Fire Yes/No Modal</DumbButton>
          </v-col>
        </v-row>

        <AlertModal :Display="ShowAlert" @Close="ShowAlert=false" />
        <YesNoModal :Display="ShowYesNo" @Result="YesNoResult" />
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import AlertModal from "@/components/Alert";
import YesNoModal from "@/components/YesNo";
import DumbButton from "@/components/DumbButton";
1;
export default {
  name: "App",
  components: { AlertModal, DumbButton, YesNoModal },
  data: () => ({
    ShowYesNo: false,
    ShowAlert: false
  }),
  methods: {
    YesNoResult(res) {
      console.log("Result from yes no modal = " + res);
      this.ShowYesNo = false;
    }
  }
};
</script>
