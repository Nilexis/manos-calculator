<template>
  <button type="button" class="fill">{{ this.text }}</button>
</template>

<script>
export default {
  name: 'FilledButton',
  props: {
    text: String
  }
}
</script>

<style scoped>
/* Fill button styling */
.fill {
  font-family: 'Karantina', cursive;
  font-size: inherit;
  font-weight: 200;
  color: #FFD166;
  letter-spacing: 1px;
  padding: 4vh 1vw 4vh 1vw;
  outline: 0;
  border: 1px solid black;
  cursor: pointer;
  position: relative;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0);
  z-index: 0;
  transition: 0.3s;
}

.fill::after {
  content: "";
  background-color: #118AB2;
  width: 100%;
  z-index: -1;
  position: absolute;
  height: 100%;
  top: 7px;
  left: 7px;
  transition: 0.3s;
}

.fill:hover::after {
  top: 0px;
  left: 0px;
}

.fill:hover {
  letter-spacing: 0.7vw;
}
/* End of Fill Button  */
</style>
