<template>
  <div>
    <NavigationBar />
    <h1>Home</h1>
    <p>Here is some information. This is the home page</p>
  </div>
</template>

<script>
import NavigationBar from '~/components/Navigation.vue'
export default {
  name: 'Home',
  components: {
    NavigationBar
  } // this is the name of the component
}
</script>
<style>
</style>
