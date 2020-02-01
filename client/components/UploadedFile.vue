<template>
  <div>
    <file-downloader :key="downloadKey" ref="downloader"></file-downloader>
    <div>
      <a
        v-bind:href="'/file/download/' + file.encodedName"
        v-on:click="downloadFile"
      >{{ file.name }}</a>
      <button v-on:click="deleteFile(file)">Delete</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import FileDownloader from "./FileDownloader.vue";

export default {
  props: ["file"],
  data() {
    return {
      downloadKey: 1
    };
  },
  name: "UploadedFile",
  methods: {
    downloadFile(event) {
      event.preventDefault();
      const url = event.target.href;
      this.downloadKey += 1;

      this.$nextTick().then(() => {
        this.$refs.downloader.downloadFile(url);
      });
    },
    deleteFile(file) {
      this.$emit("delete-file", file);
    }
  },
  components: {
    FileDownloader
  }
};
</script>

<style scoped>
</style>
