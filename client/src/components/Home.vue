<template>
  <div class="container mt-4">
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
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
