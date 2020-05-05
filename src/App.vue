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
      <h1>Styleguidist - Tutorial 2 (Into to documenting)</h1>
    </v-app-bar>

    <v-content class="ma-3">
      <v-container fill-height>
        <v-row align="center">
          <CompleteCheckmark :ShowConfetti="true" :Show="ShowCheckmark" @Done="ShowCheckmark=false">
            <span slot="message">Woohoo!</span>
            <span slot="subtitle">You like cats!</span>
            <span
              slot="body"
            >I really like cats, they are my favorite creatures! I'm glad you agree.</span>
          </CompleteCheckmark>
        </v-row>
        <v-row justify="center">
          <v-col cols="6" align="start">
            <DumbButton align="center" @clicked="ShowAlert=!ShowAlert">Fire Alert Modal</DumbButton>
          </v-col>
          <v-col cols="6" align="end">
            <DumbButton color="warning" @clicked="ShowYesNo=!ShowYesNo">Fire Yes/No Modal</DumbButton>
          </v-col>
        </v-row>

        <AlertModal
          :Display="ShowAlert"
          Header="Woah there pard!"
          Message="You clicked a button, now click another one"
          BtnColor="warning"
          @Close="ShowAlert=false"
        />
        <YesNoModal
          :Display="ShowYesNo"
          @Result="YesNoResult"
          Header="Do you like cats?"
          Message="How do you feel about cats? Do you like them?"
        />
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import AlertModal from "@/components/Alert";
import YesNoModal from "@/components/YesNo";
import DumbButton from "@/components/DumbButton";
import CompleteCheckmark from "@/components/CompleteCheckmark.vue";

export default {
  name: "App",
  components: { AlertModal, DumbButton, YesNoModal, CompleteCheckmark },
  data: () => ({
    ShowYesNo: false,
    ShowAlert: false,
    ShowCheckmark: false
  }),
  methods: {
    YesNoResult(res) {
      if (res) {
        this.ShowCheckmark = true;
      }
      this.ShowYesNo = false;
    }
  }
};
</script>
