<template>
  <div v-if="$fetchState.pending">
    Fetching post #{{ $route.params.id }}...
  </div>
  <div v-else>
    <h1>{{ post.title }}</h1>
    <pre>{{ post.body }}</pre>
    <p>
      <n-link to="/blog-index">
        Back to posts
      </n-link>
    </p>
  </div>
</template>

<script>
export default {
  async fetch () {
    this.post = await this.$http.$get(`https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}`)
  },
  data () {
    return {
      post: {}
    }
  }
}
</script>
