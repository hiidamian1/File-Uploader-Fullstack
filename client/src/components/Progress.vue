<template>
  <div class="progress">
    <div class="progress-bar progress-bar-striped bg-success" role="progressbar" v-bind:style="{width: `${percentage}%`}">
      {{percentage}}%
    </div>
  </div>
</template>

<script>
export default {
  name: "Progress",
  props: [
    "percentage"
  ]
}
</script>

<style>

</style>
