<template>
  <div class="global-sizing">
    <NavigationBar />
    <h1>Touch</h1>
    <p>Put Interaction here</p>
    <br>
    <div class="example">
      <div class="grouped">
        <button @click="counter += 1">
          Add 1
        </button>
        <p>The button above has been clicked {{ counter }} times.</p>
      </div>
    </div>
    <br>
    <div class="example">
      <!-- `greet` is the name of a method defined below -->
      <button @click="greet">
        Greet
      </button>
    </div>
    <br>
    <div class="example">
      <button @click="say('hi')">
        Say hi
      </button>
      <button @click="say('what')">
        Say what
      </button>
    </div>
    <br>
    <br>
    <div class="example">
      <button @click="warn('Form cannot be submitted yet.', $event)">
        Submit
      </button>
    </div>
    <br>
    <br>
    <div class="example">
      <!-- the click event's propagation will be stopped -->

      <!-- only trigger handler if event.target is the element itself -->
      <!-- i.e. not from a child element -->
      <div class="hit-area" @click.self="doThat">
        <button>
          Doing That
        </button>
        <!-- modifiers can be chained -->
        <a @click.stop.prevent="doThat" />
      </div>

      <a @click.stop="doThis">
        <button>
          click Stop This
        </button>
      </a>

      <!-- the submit event will no longer reload the page -->
      <form @submit.prevent="onSubmit" />

      <!-- just the modifier -->
      <form @submit.prevent />

      <!-- use capture mode when adding the event listener -->
      <!-- i.e. an event targeting an inner element is handled here before being handled by that element -->
      <div class="hit-area" @click.capture="doThis">
        <button>
          Doing This
        </button>
      </div>
    </div>
    <br>
    <br>
    <div class="example">
      <div class="grouped">
        <input class="form-item" @keyup.enter="onSubmit">
        <input class="form-item" @keyup.delete="doThis">
        <input class="form-item" @click.left="clear($event)">
      </div>
    </div>
  </div>
</template>

<script>
import NavigationBar from '~/components/Navigation.vue'
export default {
  components: {
    NavigationBar
  },
  data () {
    return {
      counter: 1,
      name: 'Vue.js'
    }
  },
  methods: {
    greet () {
      // `this` inside methods points to the Vue instance
      // alert('Hello ' + this.name + '!')
      // `event` is the native DOM event
      if (event) {
        alert('Hello ' + this.name + '!' + '\n' + event.target.tagName)
      }
    },
    say (message) {
      alert(message)
    },
    warn (message, event) {
      // now we have access to the native event

      if (event) {
        event.preventDefault()
      }
      alert(message)
    },
    doThis () {
      alert('Doing This')
    },
    onSubmit () {
      location.reload()
    },
    doThat () {
      alert('Doing That')
    },
    clear (event) {
      alert(event.target.tagName)
    }
  }
}
</script>
<style>
.example {
  background-color: cyan;
  margin: 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.grouped {
  background-color:thistle;
  padding: 25px;
  margin: 0 auto;
  display: grid;
  text-align: center;
}

.form-item {
  padding: 10px;
}

.hit-area {
  background-color: beige;
  padding: 25px;
  margin: 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

</style>
