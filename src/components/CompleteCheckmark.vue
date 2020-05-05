<template>
  <v-expand-transition>
    <div v-show="StartTransistion">
      <v-row>
        <v-col align="center">
          <v-icon size="400" color="success">mdi-check-circle-outline</v-icon>
        </v-col>
      </v-row>
      <v-row>
        <v-col align="center">
          <h1>
            <slot name="message"></slot>
          </h1>
        </v-col>

        <v-col align="center">
          <h2>
            <slot name="subtitle"></slot>
          </h2>
        </v-col>

        <v-col align="center">
          <p>
            <slot name="body"></slot>
          </p>
        </v-col>
      </v-row>
    </div>
  </v-expand-transition>
</template>

<script>
export default {
  name: "CompleteCheckmark",
  data() {
    return {
      StartTransistion: false
    };
  },
  props: {
    ShowConfetti: {
      default: false
    },

    ConfettiTimeout: {
      default: 1000
    },

    Show: {
      default: false
    },

    DisplayTime: {
      default: 2000
    },

    Msg: {
      default: "Success!"
    }
  },
  mounted() {
    setTimeout(() => {
      if (this.Show) {
        this.StartTransistion = true;
      }
    }, 100);

    this.MakeConfettiHappen();
  },
  watch: {
    Show: function(val) {
      this.StartTransistion = val;

      this.MakeConfettiHappen();
    },
    StartTransistion: function(val) {
      if (val) {
        setTimeout(() => {
          this.StartTransistion = false;
          this.$emit("Done");
        }, this.DisplayTime);
      }
    }
  },
  computed: {
    Show_Confetti() {
      if (typeof this.ShowConfetti == "string") {
        return this.ShowConfetti.toLowerCase() === "true";
      } else {
        return this.ShowConfetti;
      }
    }
  },
  methods: {
    MakeConfettiHappen() {
      if (!this.Show_Confetti || !this.StartTransistion) {
        this.$confetti.stop();
        return;
      }

      this.$confetti.update({
        particles: [
          {
            type: "circle"
          },
          {
            type: "rect"
          }
        ],
        customCanvas: false,
        particlesPerFrame: 5,
        defaultDropRate: 100
      });
      this.$confetti.start();

      setTimeout(() => this.$confetti.stop(), this.ConfettiTimeout);
    }
  }
};
</script>

<style scoped>
.font-xxl {
  font-size: 96pt;
}
</style>
