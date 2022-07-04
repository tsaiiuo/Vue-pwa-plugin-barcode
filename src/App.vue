<template>
  <StreamBarcodeReader
    @decode="onDecode"
    @loaded="onLoaded"
    :camera="front"
  ></StreamBarcodeReader>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import { StreamBarcodeReader } from "vue-barcode-reader";
export default {
  name: "App",
  components: {
    HelloWorld,
    StreamBarcodeReader,
  },
  methods: {
    onDecode(result) {
      if (result === "172018300784437") {
        return;
      }
      console.log(result);
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
