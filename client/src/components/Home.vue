<template>
  <div class="container mt-4 mb-4">
    <h4 class="display-4 text-center mb4">
      <i class="fab fa-vuejs"></i> Vue File Uploader
    </h4>
    <FileUploader/>
  </div>
</template>

<script>
import FileUploader from "./FileUploader";

export default {
  name: 'Home',
  components: {
    FileUploader
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
