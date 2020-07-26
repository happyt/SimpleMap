<template>
  <div class="mapPage">
    <h1>Main Map</h1>
    <p>Please click a section</p>
    <select v-model="selected">
      <option
        v-for="(option,index) in options"
        v-bind:value="option.value"
        :key="index"
      >{{ option.text }}</option>
    </select>

    <div>
      <main-map v-on:map-clicked="onMapClick" :pickColour="selected" :allColours="fullSet"></main-map>
    </div>
  </div>
</template>

<script>
import MainMap from "./MainMap.vue";
export default {
  name: "MapPage",
  components: {
    MainMap,
  },
  data: function () {
    return {
      selected: "none",
      fullSet: ["none", "abc", "def"],
      options: [
        { text: "Default", value: "none" },
        { text: "ABC", value: "abc" },
        { text: "DEF", value: "def" },
      ],
    };
  },
  props: {
    msg: String,
  },
  methods: {
    onMapClick: function (attr) {
      this.$notify({
        group: "map",
        title: "Map clicked",
        text: `Clicked id: ${attr.mapId}, title: ${attr.title}, onOff: ${attr.onOff}`,
      });
    },
  },
};
</script>
