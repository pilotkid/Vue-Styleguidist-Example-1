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
          <h1>{{Msg}}</h1>
        </v-col>
      </v-row>
    </div>
  </v-expand-transition>
</template>

<script>
/**
 * This is a large checkmark in a circle centered on the screen
 */
export default {
  name: "CompleteCheckmark",
  data() {
    return {
      StartTransistion: false
    };
  },
  props: {
    /**
     * Shows confetti when the screen is displayed
     * @values `true`,`false`
     */
    ShowConfetti: {
      default: false
    },

    /**
     * This is how long the confetti should fall
     * @values 1000+
     */
    ConfettiTimeout: {
      default: 1000
    },

    /**
     * Shows the item with the animation
     * @values `true`,`false`
     */
    Show: {
      default: false
    },

    /**
     * How long to show the completed screen
     *
     * **Should be 2x the confetti time**
     * @values 2000+
     */
    DisplayTime: {
      default: 2000
    },

    /**
     * Message to be displayed
     */
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
          /**
           *This notifies that the animation has been completed
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

<docs>
```vue
let ShowConfettiSwitch = false;
let ShowComplete = false;
 
<v-switch v-model="ShowConfettiSwitch" label="Show Confetti"></v-switch >
<v-btn color="primary" @click="ShowComplete=!ShowComplete">{{show ? "Hide":"Show"}}</v-btn>

<CompleteCheckmark 
    :ShowConfetti="ShowConfettiSwitch" 
    :Show="ShowComplete"
    @Done="ShowComplete = false"
    >
Woo! You clicked the Show button!
</CompleteCheckmark>

```
</docs>