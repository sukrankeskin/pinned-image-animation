<template>
  <PinnedmageVue />
</template>

<script>
import PinnedmageVue from "./components/Pinnedmage.vue";
export default {
  name: "App",
  components: {
    PinnedmageVue,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
