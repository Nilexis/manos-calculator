<template>
  <div>
    <p>...מחשב מנוס</p>
    <div class="bar">
      <div :style="{ width: `${Math.min(progress, 100)}%` }" />
    </div>
  </div>
</template>

<script>
export default {
  name: "RetroProgressBar",
  props: {
    progress: Number,
  },
};
</script>

<style scoped>
.bar {
  display: block;
  margin-left: auto;
  margin-right: auto;
  background-color: black;
  padding: 3px;
  width: 50vw;
}

.bar > div {
  background-color: #118AB2;
  width: 40%;
  height: 50px;
  transition: width 0.5s ease-out;
}

p {
  font-family: "Karantina", cursive;
  font-size: 10vw;
  margin: 0;
}
</style>
