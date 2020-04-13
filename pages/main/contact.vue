<template>
  <div class="global-sizing">
    <NavigationBar />
    <h1>Contact Me</h1>
    <p>
      <ul>
        <li>Email: {{ email }}</li>
        <li>Website: {{ web }}</li>
      </ul>
    </p>
  </div>
</template>

<script>
import NavigationBar from '~/components/Navigation.vue'
export default {
  name: 'Contact',
  components: {
    NavigationBar
  },
  data () {
    return {
      email: 'atn010g@gmail.com',
      web: 'atn010.com'
    }
  }
}
</script>
