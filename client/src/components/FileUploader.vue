<template>
  <div>
    <Message v-if="alertMessage" @dismissed="alertMessage = ''" v-bind:message="alertMessage"/>

    <form enctype="multipart/form-data" @submit="uploadFile">
      <div class="custom-file mb-4">
        <input type="file" class="custom-file-input" id="customFile" v-on:change="setFile">
        <label class="custom-file-label" for="customFile">{{inputString}}</label>
      </div>

      <Progress v-bind:percentage="uploadPercentage"/>

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
import Message from "./Message";
import Progress from "./Progress";

export default {
  name: "FileUploader",
  components: {
    Message,
    Progress
  },
  data() {
    return {
      inputString: "Choose File",
      inputFilePath: "",
      alertMessage: "",
      uploadPercentage: 0
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
          },
          onUploadProgress: progress => {
            this.uploadPercentage = parseInt(Math.round((progress.loaded * 100) / progress.total));

            setTimeout(() => this.uploadPercentage = 0, 10000);
          }
        });

        this.inputFilePath = response.data.filePath;
        this.alertMessage = "File uploaded";

      } catch(err) {
        if (err.response.status === 500) {
          this.alertMessage = "Server problem"
        } else {
          this.alertMessage = err.response.data.msg;
        }
      }
    }
  }
}
</script>

<style scoped>

</style>
