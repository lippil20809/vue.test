<template>
  <header>
    <h2>THEME</h2>
    <h2>DARK</h2>
    <h2>LIGHT</h2>
    <ToggleWrapper :mode="mode" @toggle="$emit('toggle')" />
  </header>
</template>

<script>
import ToggleWrapper from "./ToggleWrapper.vue";
export default {
  props: ["mode"],
  components: {
    ToggleWrapper,
  },
};
</script>

<style>
header {
  display: flex;
  padding-top: 60px;
  padding-left: 25px;
}

h2:nth-child(2) {
  padding-left: 29px;
  padding-right: 15px;
}

h2:nth-child(3) {
  padding-right: 15px;
}
</style>
