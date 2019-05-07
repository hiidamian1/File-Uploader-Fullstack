<template>
  <div class="alert alert-info alert-dismissible fade show" role="alert">
    {{message}}
    <button v-on:click="dismiss" type="button" class="close" data-dismiss="alert" aria-label="Close">
      <span aria-hidden="true">&times;</span>
    </button>
  </div>
</template>

<script>
export default {
  name: "Message",
  props: [
    "message"
  ],
  methods: {
    dismiss(event) {
      this.$emit("dismissed");
    }
  }
}
</script>

<style>

</style>
