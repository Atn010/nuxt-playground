<template>
  <div>
    <div class="grouper">
      <nuxt-link to="/">
        <a href="" target="_blank" class="navButton--grey">
          <Logo height="50px" width="50px" />
        </a>
      </nuxt-link>
      <div class="nav_links">
        <h2>Nav Bar</h2>
        <router-link
          v-for="routes in links"
          :key="routes.id"
          :to="`${routes.page}`"
        >
          <a href="" target="_blank" class="navButton--grey">
            {{ routes.text }}
          </a>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
export default {
  name: 'Navigation',
  components: {
    Logo
  },
  data () {
    return {
      links: [
        {
          id: 1,
          text: 'Home',
          page: '/main/home'
        },
        {
          id: 2,
          text: 'Touch',
          page: '/main/touch'
        },
        {
          id: 3,
          text: 'Whiteboard',
          page: '/main/whiteboard'
        },
        {
          id: 6,
          text: 'Currency Converter',
          page: '/main/currencycon'
        },
        {
          id: 4,
          text: 'About',
          page: '/main/about'
        },
        {
          id: 5,
          text: 'Contact',
          page: '/main/contact'
        },
        {
          id: 7,
          text: 'Blog',
          page: '/blog-index'
        }
      ]
    }
  }
}
</script>

<style>
.grouper {
    background: darkslategray;
  margin: 15 auto;
  display: flex;
  justify-content: left;
  align-items: center;
  text-align: center;
}

.navButton--grey {
  display: inline-block;
  background-color: white;
  border: 1px solid grey;
  color: black;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}

.navButton--grey:hover {
  color: #fff;
  background-color: #35495e;
}
.

.nav_links {
  padding-top: 15 auto;
}
</style>
