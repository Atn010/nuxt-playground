<template>
  <div>
    <ul v-for="(item, index) in currencies" :key="index">
      <li>
        {{ item }} - {{ amount * data.rates[item] }}
        <br>
        1 {{ current }} = {{ item }} {{ data.rates[item] }}
      </li>
      <br>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    current: {
      type: String,
      default: 'USD'
    },
    data: {
      type: Object,
      default: {} === ({ USD: 1 })
    },
    currencies: {
      type: Array,
      default: [] === ['USD']
    },
    amount: {
      type: Number,
      default: 1
    },
    mounted () {
      console.log(this.data)
    }
  }
}
</script>

<style lang="sass" scoped>

</style>
