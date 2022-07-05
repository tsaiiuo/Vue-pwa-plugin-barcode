<template>
  <h1 class="text-3xl font-bold">The decoded value in QR/barcode is</h1>
  <h1 class="text-2xl font-bold p-3">{{ result }}</h1>
  <button
    @click.prevent="start"
    class="bg-green-500 py-2 px-8 text-xl font-bold mb-5"
  >
    start/close
  </button>
  <StreamBarcodeReader
    v-if="isVisual"
    @decode="onDecode"
    @loaded="onLoaded"
    :camera="front"
  ></StreamBarcodeReader>
  <h1 class="text-2xl font-bold p-5">npm: vue-barcode-reader</h1>
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
  data() {
    return {
      result: "",
      isVisual: false,
    };
  },
  methods: {
    onDecode(result) {
      if (result === "172018300784437") {
        return;
      }
      this.result = result;
    },
    start() {
      this.isVisual = !this.isVisual;
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
