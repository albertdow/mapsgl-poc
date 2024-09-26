<template>
  <div style="height:600px; width:800px">
    <l-map ref="map" id="map" v-model:zoom="zoom" :center="[47.41322, -1.219482]" @ready="readyFunction">
      <l-tile-layer url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png" layer-type="base"
        name="OpenStreetMap"></l-tile-layer>
    </l-map>
  </div>

</template>

<script>

import "leaflet/dist/leaflet.css";
import { LMap, LTileLayer } from "@vue-leaflet/vue-leaflet";
import * as mapsgl from '@aerisweather/mapsgl';
//  controller.addWeatherLayer("radar");
//});
export default {
  name: 'App',
  components: {
    LMap,
    LTileLayer,
  },
  data() {
    return {
      zoom: 2,
      map: null,
    };
  },
  methods: {
    setupAerisMapgl(map) {
      const account = new mapsgl.Account(
        "CLIENT_ID",
        "CLIENT_SECRET"
      );
      const controller = new mapsgl.LeafletMapController(map, {
        account,
      });
      controller.on("load", () => {
        controller.addWeatherLayer("radar");
      });
    },
    readyFunction(map) {
      this.setupAerisMapgl(map);
    }
  },
}
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
