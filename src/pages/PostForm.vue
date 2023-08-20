<template>
  <p>
    <RouterLink to="/" class="btn btn-outline-secondary"
      >Go back to list</RouterLink
    >
  </p>
  <pre>
    {{ model }}
  </pre>
  <div>
    <form @submit.prevent="onSubmit">
      <h1>{{ model.id ? "Edit Post" : "Create new Post" }}</h1>
      <div class="mb-3">
        <input
          type="text"
          class="form-control"
          placeholder="Post Title"
          v-model="model.title"
        />
      </div>
      <div class="mb-3">
        <textarea
          tyoe="text"
          class="form-control"
          placeholder="Post Body"
          v-model="model.body"
        ></textarea>
      </div>
      <p>
        <button
          class="btn btn-success"
          type="submit"
          :disabled="!model.title || !model.body"
        >
          Submit
        </button>
      </p>
    </form>
  </div>
</template>

<script setup>
  import { ref, onMounted } from "vue"
  import { useRoute, useRouter } from "vue-router"
  import store from "../store"

  const router = useRouter()
  const route = useRoute()

  const model = ref({
    id: "",
    title: "",
    body: "",
  })

  onMounted(async () => {
    if (!route.params.id) {
      return
    }

    model.value = await store.dispatch("getSinglePost", route.params.id)

    // fetch("https://jsonplaceholder.typicode.com/posts/" + route.params.id)
    //   .then((res) => res.json())
    //   .then((post) => (model.value = post))
  })

  function onSubmit() {
    store.dispatch("savePost", model.value).then((res) => router.push("/"))
    // if (model.value.id) {
    //   fetch("https://jsonplaceholder.typicode.com/posts/" + model.value.id, {
    //     method: "PUT",
    //     body: JSON.stringify(model.value),
    //   })
    //     .then((res) => res.json())
    //     .then((res) => {
    //       router.push("/")
    //     })
    // } else {
    //   fetch("https://jsonplaceholder.typicode.com/posts/", {
    //     method: "POST",
    //     body: JSON.stringify(model.value),
    //   })
    //     .then((res) => res.json())
    //     .then((res) => {
    //       router.push("/")
    //     })
    // }
  }
</script>

<style></style>
