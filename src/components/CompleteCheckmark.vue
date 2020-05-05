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
            <!-- @slot This is for your big message -->
            <slot name="message"></slot>
          </h1>
        </v-col>

        <v-col align="center">
          <h2>
            <!-- @slot This is for smaller than title text -->
            <slot name="subtitle"></slot>
          </h2>
        </v-col>

        <v-col align="center">
          <p>
            <!-- @slot Use this for a regular paragraph sized text below the subtitle -->
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
    /**
     * This will allow confetti to fall on the screen
     * @values true, false
     */
    ShowConfetti: {
      default: false
    },

    /**
     * This is how long confetti will be shown
     * @values 1000+
     */
    ConfettiTimeout: {
      default: 1000
    },

    /**
     * This is if the checkmark will be shown
     * @values true, false
     */
    Show: {
      default: false
    },

    /**
     * How long the checkmark is displayed
     * @values 2000+ ( or 2x the confetti timeout )
     */
    DisplayTime: {
      default: 2000
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

          /**
           * This notifies the parent that the animation is complete
           */
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
