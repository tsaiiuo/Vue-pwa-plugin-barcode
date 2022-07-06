<template>
  <div class="flex flex-col justify-center items-center group w-full">
    <img
      v-if="!isVisual"
      class="animate-bounce"
      src="./assets/logo.png"
      alt=""
    />
    <h1 v-if="!isVisual" class="text-3xl font-bold p-5 mb-4">
      Vue-barcode/qrcode-reader
    </h1>
    <h1 v-if="isVisual" class="text-3xl font-bold">
      The decoded value in QR/barcode is
    </h1>
    <h1 v-if="isVisual" class="text-2xl font-bold p-3">{{ result }}</h1>
    <StreamBarcodeReader
      class="w-full"
      v-if="isVisual"
      @decode="onDecode"
      @loaded="onLoaded"
      :camera="front"
    ></StreamBarcodeReader>
    <button
      @click.prevent="start"
      class="bg-green-500 py-2 px-8 text-xl font-bold group-hover:scale-110 mt-3 transition delay-150 duration-300 ease-in-out"
    >
      start/close
    </button>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import { StreamBarcodeReader } from "./vue-barcode-reader/src/index";
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
