<template>
  <div id="app">
    <GoogleMapPolygon />
  </div>
</template>

<script>
import GoogleMapPolygon from "./components/Polygon";

export default {
  name: "App",
  components: {
    GoogleMapPolygon,
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
