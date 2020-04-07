<template>
  <div>
    <NavigationBar />
    <h1>Whiteboard</h1>
    <p>Have fun and draw something</p>
    <div class="background">
      <canvas ref="canvas" class="whiteboard" height="250vh" width="1000px" @click.self="onClick($event)" />
    </div>
  </div>
</template>

<script>
import NavigationBar from '~/components/Navigation.vue'
export default {
  name: 'Whiteboard',
  components: {
    NavigationBar
  }, // this is the name of the component
  data () {},
  mounted () {},
  methods: {
    onClick (event) {
      const x = event.clientX // Get the horizontal coordinate
      const y = event.clientY // Get the vertical coordinate
      const canvs = this.$refs.canvas
      const context = canvs.getContext('2d')
      const colorArray = ['#FF0000', '#00FF00', '#0000FF', '#FFFF00', '#00FFFF', '#FF00FF', '#000000']
      context.fillStyle = colorArray[Math.floor(Math.random() * 7)]
      context.fillRect(((x - 25) - canvs.offsetLeft), ((y - 25) - canvs.offsetTop), 50, 50)
    }
  }
}
</script>
<style>

.whiteboard {
  background-color: white;
  border: 2px black;
  margin: 0 auto;
  display: flex;
}

.background {
  background-color: beige;
  padding: 25px;
  border: black;
  border-width: 10vh;
  margin: 0 auto;
  display: flex;
}

</style>
