<template>
  <div id="app">
    <notifications group="map" />
    <MapPage msg="My little app" />
  </div>
</template>

<script>
import MapPage from "./components/MapPage.vue";

export default {
  name: "app",
  components: {
    MapPage,
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
