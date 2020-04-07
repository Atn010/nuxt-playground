<template>
  <div>
    <NavigationBar />
    <h1>About</h1>
    <p>Here is some information. This is the about page</p>
  </div>
</template>

<script>
import NavigationBar from '~/components/Navigation.vue'
export default {
  name: 'About',
  components: {
    NavigationBar
  } // this is the name of the component
}
</script>
<style>
</style>
