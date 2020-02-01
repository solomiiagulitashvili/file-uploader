<template>
  <div>
    <h1>Files List</h1>

    <ul>
      <uploaded-file v-for="file in files" v-bind:file.sync="file"></uploaded-file>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import UploadedFile from "./UploadedFile.vue";

export default {
  name: "UploadedFilesList",
  data() {
    return {
      files: []
    };
  },
  components: {
    UploadedFile
  },
  methods: {
    fetchFiles() {
      const self = this;
      axios.get("/api/files").then(response => {
        this.$set(this, "files", response.data);
      });
    },
    filesUploaded(files) {
      files.forEach(file => {
        this.files.push(file);
      });
    }
  },
  mounted() {
    this.fetchFiles();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
