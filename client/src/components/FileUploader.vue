<template>
  <div>
    <form enctype="multipart/form-data" @submit="uploadFile">
      <div class="custom-file">
        <input type="file" class="custom-file-input" id="customFile" v-on:change="setFile">
        <label class="custom-file-label" for="customFile">{{inputString}}</label>
      </div>

      <input type="submit" value="Upload File" class="btn btn-primary btn-block mt-4"/>
    </form>

    <div v-if="inputFilePath" class="row mt-5">
      <div class="col-md-6 m-auto">
        <h3 class="text-center">
          {{this.inputString}}
        </h3>
        <img v-bind:src="inputFilePath" style="width: 100%">
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "FileUploader",
  data() {
    return {
      inputString: "Choose File",
      inputFilePath: ""
    }
  },
  methods: {
    setFile(event) {
      this.inputString = event.target.files[0].name;
      this.inputFile = event.target.files[0];
    },
    async uploadFile(event) {
      event.preventDefault();
      const formData = new FormData();
      formData.append("file", this.inputFile);
    
      try {
        const response = await axios.post("upload", formData, {
          headers: {
            "Content-Type": "multipart/form-data"
          }
        });

        this.inputFilePath = response.data.filePath;
      } catch(err) {
        if (err.response.status === 500) {
          console.log("server problem")
        } else {
          console.log(err.response.data.msg);
        }
      }
    }
  }
}
</script>

<style scoped>

</style>
