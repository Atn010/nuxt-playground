<template>
  <div class="global-sizing">
    <NavigationBar />
    <h1>Blog posts</h1>
    <p v-if="$fetchState.pending">Fetching posts...</p>
    <p v-else-if="$fetchState.error">Error while fetching posts: {{ $fetchState.error.message }}</p>
    <ul v-else>
      <li v-for="post of posts" :key="post.id">
        <n-link :to="`/post/${post.id}`">{{ post.title }}</n-link>
      </li>
    </ul>
  </div>
</template>

<script>
import NavigationBar from '~/components/Navigation.vue'
export default {
  components: {
    NavigationBar
  },
  async fetch () {
    this.posts = await this.$http.$get('https://jsonplaceholder.typicode.com/posts')
  },
  data () {
    return {
      posts: []
    }
  }
}
</script>
