<template>
  <div
    id="overview-container"
    style="width:100%;height:250px;"
    ref="overview"
  ></div>
  <div
    id="zoomview-container"
    style="width:100%;height:250px;"
    ref="zoomview"
  ></div>
  <audio
    src="drmapan.wav"
    style="width:100%"
    controls
  ></audio>
  <div>
    <button @click="zoomIn">Zoom in</button>
    <button @click="zoomOut">Zoom out</button>
  </div>
</template>

<script>
import Peaks from "peaks.js";
export default {
  name: "App",
  data() {
    return {
      peakInstance: null,
    };
  },
  mounted() {
    this.createPeakInstance();
  },
  methods: {
    createPeakInstance() {
      const options = {
        containers: {
          overview: document.getElementById("overview-container"),
          zoomview: document.getElementById("zoomview-container"),
        },
        mediaElement: document.querySelector("audio"),
        dataUri: {
          arraybuffer: "drmapan.dat", 
        },
        zoomLevels: [8, 16, 32, 64, 128, 256, 512],
      };
      const vm = this;
      Peaks.init(options, function (err, peaks) {
        console.log(err, peaks);
        vm.peakInstance = peaks;
      });
    },
    zoomIn() {
      this.peakInstance.zoom.zoomIn();
    },
    zoomOut() {
      this.peakInstance.zoom.zoomOut();
    },
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
