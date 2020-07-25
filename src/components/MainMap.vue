<template>
  <div>
    <div>{{pickColour}}</div>
    <div :id="svgId" class="svg-container"></div>
  </div>
</template>

<script>
import myMap from "../assets/MainMap";
export default {
  name: "VenueMapComponent",
  props: {
    pickColour: String,
  },
  data: function () {
    return {
      svgId: "myMap",
      mapAttr: {
        viewBoxWidth: 1106,
        viewBoxHeight: 500,
        imageWidth: 1106,
        imageHeight: 500,
      },
      svgContainer: null,
    };
  },
  mounted: function () {
    this.generateVenueMap();
  },
  methods: {
    generateVenueMap: function () {
      const vue = this;
      const mapData = myMap.g.path;
      const svgContainer = vue
        .$svg("myMap")
        .size("100%", "100%")
        .viewbox(-200, 0, vue.mapAttr.viewBoxWidth, vue.mapAttr.viewBoxHeight);
      vue.svgContainer = svgContainer;
      mapData.forEach((pathObj) => {
        vue.generatePath(svgContainer, pathObj);
      });
    },
    generatePath: function (svgCont, pathObj) {
      const vue = this;
      const attrs = {
        title: pathObj["-title"],
        "map-id": pathObj["-id"],
      };
      const element = svgCont.path(pathObj["-d"]).attr(attrs);

      let mapId = "";
      let title = "";
      element.click(function () {
        mapId = this.node.attributes["map-id"].value;
        title = this.node.attributes["title"].value;

        // need a way to set string from property
        this.node.classList.toggle("abc");

        vue.$emit("map-clicked", { mapId, title });
      });
      element.mouseover(function () {
        mapId = this.node.attributes["map-id"].value;
        title = this.node.attributes["title"].value;
        this.node.classList.add("on");
        //     vue.$emit("map-over", { mapId, title });
      });
      element.mouseout(function () {
        mapId = this.node.attributes["map-id"].value;
        title = this.node.attributes["title"].value;
        this.node.classList.remove("on");
        //     vue.$emit("map-over", { mapId, title });
      });
    },
  },
};
</script>
<style>
path {
  fill: #adaf93;
  stroke: white;
}
path.on {
  fill: rgb(221, 221, 103);
  stroke: rgb(128, 98, 16);
}
path.abc {
  fill: rgb(47, 80, 48);
  stroke: rgb(25, 100, 71);
}
path.abc.on {
  fill: rgb(102, 182, 104);
  stroke: rgb(25, 100, 71);
}
</style>
