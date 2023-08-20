<template>
  <pre>
  {{ postList }}
  </pre>
</template>

<script setup>
  import { onMounted, ref } from "vue"

  const postList = ref([])

  onMounted(() => {
    fetch("https://jsonplaceholder.typicode.com/posts")
      .then((res) => res.json())
      .then((posts) => (postList.value = posts))
  })
</script>

<style></style>
