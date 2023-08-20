<template>
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
  import { useRoute } from "vue-router"

  const route = useRoute()

  const model = ref({
    id: "",
    title: "",
    body: "",
  })

  onMounted(() => {
    if (!route.params.id) {
      return
    }
    fetch("https://jsonplaceholder.typicode.com/posts/" + route.params.id)
      .then((res) => res.json())
      .then((post) => (model.value = post))
  })
</script>

<style></style>
