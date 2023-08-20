<template>
  <!-- <pre>
  {{ postList }}
  </pre> -->
  <div>
    <PostItem
      v-for="post of postList"
      :key="post.id"
      :post="post"
      @delete="onDelete(post)"
    />
  </div>
</template>

<script setup>
  import { onMounted, ref } from "vue"
  import PostItem from "../components/PostItem.vue"

  const postList = ref([])

  onMounted(() => {
    fetch("https://jsonplaceholder.typicode.com/posts")
      .then((res) => res.json())
      .then((posts) => (postList.value = posts))
  })

  function onDelete(post) {
    postList.value = postList.value.filter((p) => p.id != post.id)
  }
</script>

<style></style>
