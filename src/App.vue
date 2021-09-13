<template>
  <div id="app">
    <transition name="fade">
      <h1 v-show="!isCalculating && !isCalculationFinished" class="header">
        מחשבון מנוס
      </h1>
    </transition>
    <transition name="shrink-fade">
      <div
        class="center-vertical main-button"
        v-show="!isCalculating && !isCalculationFinished"
        @click="!isCalculating && startCalculation()"
      >
        <filled-button :text="'?יש מנוס'" />
      </div>
    </transition>

    <transition name="shrink-fade">
      <retro-progress-bar
        class="center-vertical progress-bar"
        v-show="isCalculating && !isCalculationFinished"
        :progress="progressAmount"
      />
    </transition>

    <transition name="shrink-fade">
      <div
        class="center-vertical manos-res"
        v-show="!isCalculating && isCalculationFinished"
      >
        <manos-result :isPositive="isPositive" />
        <div
          class="sec-button"
          @click="!isCalculating && (isCalculationFinished = false)"
        >
          <filled-button :text="'?שננסה שוב'" />
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import FilledButton from "./components/FilledButton.vue";
import RetroProgressBar from "./components/RetroProgressBar.vue";
import ManosResult from "./components/ManosResult.vue";

export default {
  name: "App",
  components: {
    FilledButton,
    RetroProgressBar,
    ManosResult,
  },
  data() {
    return {
      isCalculating: false,
      isCalculationFinished: false,
      progressAmount: 0,
      isPositive: false,
    };
  },
  methods: {
    async startCalculation() {
      this.isCalculating = true;
      this.progressAmount = 0;

      const MAX_PROGRESSION = 100;

      await this.sleep(500);

      while (this.progressAmount < MAX_PROGRESSION) {
        const addedProgress = Math.min(
          -Math.log(Math.random()) / Math.log(100),
          1
        );

        this.progressAmount = Math.min(
          this.progressAmount + (addedProgress * MAX_PROGRESSION) / 8,
          MAX_PROGRESSION
        );
        await this.sleep(100);
      }

      await this.sleep(500);

      this.isCalculating = false;

      this.showResult();
    },
    async sleep(ms) {
      return new Promise((res) => setTimeout(res, ms));
    },
    showResult() {
      this.isPositive = Math.random() > 0.5;
      this.isCalculationFinished = true;
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Karantina:wght@300&display=swap");


#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0;
  padding: 0;
  background-color: #ffd166;
  height: 100%;
  position: relative;
}

html,
body {
  font-family: "Karantina", cursive;
  height: 100%;
  margin: 0;
  padding: 0;
}

.header {
  font-family: "Karantina", cursive;
  color: #073b4c;
  font-size: 25vmin;
  font-weight: 500;
  margin: 0;
  padding: 0;
}

.center-vertical {
  position: absolute;
  top: 50%;
  left: 50%;
  margin: 0;
  transform: translate(-50%, -50%);
}

.main-button {
  width: 50vmin;
  font-size: 15vmin;
}

.sec-button {
  width: 40vmin;
  font-size: 10vmin;
  margin: 5vh auto auto auto;
}

.manos-res {
  width: 100%;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.shrink-fade-enter-active,
.shrink-fade-leave-active {
  transition: opacity 0.5s ease-in-out, transform 0.5s;
}
.shrink-fade-enter,
.shrink-fade-leave-to {
  opacity: 0;
  transform: translateX(-50%) translateY(-50%) scale(0.5);
}


@media (max-aspect-ratio: 7/8) {
  .header {
    font-size: 30vw;
  }
}
</style>
