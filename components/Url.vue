<template>
  <div class="w[100%]">
    <p>{{ url }}</p>
    <p>{{ timestamp }}</p>
    <p>{{ mimeType }}</p>
    <p>{{ statusCode }}</p>
  </div>
</template>
<script>
export default {
  name: 'url',
  props: {
    url: {
      type: String,
      required: true
    },
    timestamp: {
      type: String,
      required: true
    },
    mimeType: {
      type: String,
      required: true
    },
    statusCode: {
      type: String,
      required: true
    },
  },
}
</script>

<style scoped>

</style>
