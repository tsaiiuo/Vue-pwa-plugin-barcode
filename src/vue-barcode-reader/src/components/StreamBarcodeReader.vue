<template>
  <div class="scanner-container">
    <div v-show="!isLoading">
      <video poster="data:image/gif,AAAA" ref="scanner"></video>
      <div></div>
      <div class="laser"></div>
    </div>
  </div>
</template>

<script>
import { BrowserMultiFormatReader, Exception } from "@zxing/library";

export default {
  name: "stream-barcode-reader",

  data() {
    return {
      isLoading: true,
      codeReader: new BrowserMultiFormatReader(),
      isMediaStreamAPISupported:
        navigator &&
        navigator.mediaDevices &&
        "enumerateDevices" in navigator.mediaDevices,
    };
  },

  mounted() {
    if (!this.isMediaStreamAPISupported) {
      throw new Exception("Media Stream API is not supported");
      return;
    }

    this.start();
    this.$refs.scanner.oncanplay = (event) => {
      this.isLoading = false;
      this.$emit("loaded");
    };
  },

  beforeUnmount() {
    this.codeReader.reset();
  },

  methods: {
    start() {
      this.codeReader.decodeFromVideoDevice(
        undefined,
        this.$refs.scanner,
        (result, err) => {
          if (result) {
            this.$emit("decode", result.text);
          }
        }
      );
    },
  },
};
</script>

<style scoped>
video {
  max-width: 100%;
  max-height: 100%;
}
.scanner-container {
  position: relative;
}

.laser {
  width: 100%;
  background-color: tomato;
  height: 1px;
  position: absolute;
  top: 40%;
  z-index: 2;
  box-shadow: 0 0 4px red;
  -webkit-animation: scanning 2s infinite;
  animation: scanning 2s infinite;
}
@-webkit-keyframes scanning {
  50% {
    -webkit-transform: translateY(100px);
    transform: translateY(100px);
  }
}
@keyframes scanning {
  50% {
    -webkit-transform: translateY(100px);
    transform: translateY(100px);
  }
}
</style>
