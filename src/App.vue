<template>
  <div class="app" :class="mode">
    <HeaderText :mode="mode" @toggle="toggle" />
    <DropDown />
  </div>
</template>

<script>
import HeaderText from "./components/HeaderText.vue";
import DropDown from "./components/DropDown.vue";

export default {
  name: "app",
  data() {
    return {
      mode: "dark",
    };
  },
  components: {
    HeaderText,
    DropDown,
  },
  methods: {
    toggle() {
      if (this.mode === "dark") {
        this.mode = "light";
      } else {
        this.mode = "dark";
      }
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-weight: 400;
  font-size: 13px;
  line-height: 15.23px;
  font-family: "Roboro", sans-serif;
  letter-spacing: 1.5px;
}

.app {
  width: 100vw;
  min-height: 100vh;
  background-color: #ffffff;
  color: #000000;
}

.app li:hover {
  background-color: #86d4e8;
}

.app .selected-item {
  border: 1px solid #c4c4c4;
}

.app .dropdown-popover {
  border: 1px solid #c4c4c4;
}

.dark {
  background-color: #181f29;
  color: #ffffff;
}
.dark .selected-item {
  border: 1px solid #0e1319;
}
.dark .dropdown-popover {
  border: 1px solid #0e1319;
}

.dark li:hover {
  background-color: #12171f;
  color: #86d4e8;
}
</style>
