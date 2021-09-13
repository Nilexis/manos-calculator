<template>
  <div>
    <p class="main-text" :class="{ green: isPositive, red: !isPositive }">
      {{ textData[selected].main }}
    </p>
    <p class="subtext">{{ textData[selected].sec }}</p>
  </div>
</template>

<script>
export default {
  name: "FilledButton",
  props: {
    isPositive: String,
  },
  data() {
    return {
      textData: {
        positive: {
          main: ".יש מנוס",
          sec: "נמצא מנוס על ידי המערכת",
        },
        negative: {
          main: ".אין מנוס",
          sec: "המערכת לא מצאה מנוס",
        },
      },
    };
  },
  computed: {
    selected() {
      return this.isPositive ? "positive" : "negative";
    },
  },
};
</script>

<style scoped>
.subtext {
  font-family: "Karantina", cursive;
  font-size: 10vmin;
  margin: 0;
}

.main-text {
  font-family: "Karantina", cursive;
  font-size: 30vmin;
  margin: 0;
}

.red {
  color: #ef476f;
}

.green {
  color: #06d6a0;
}
</style>
