<template>
  <div id="app">
    <PolygonWithLabel />
  </div>
</template>

<script>
import PolygonWithLabel from "./components/PolygonWithLabel";

export default {
  name: "App",
  components: {
    PolygonWithLabel,
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
