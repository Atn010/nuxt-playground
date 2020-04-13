<template>
  <div>
    <ul v-for="(item, index) in currencies" :key="index">
      <li>
        <br>
        <Row
          :current="current"
          :currency="item"
          :rate="data.rates[item]"
          :amount="amount"
        />
        <br>
      </li>
      <br>
    </ul>
  </div>
</template>

<script>
import Row from '~/components/row.vue'

export default {
  components: {
    Row
  },
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
    }
  }
}
</script>

<style lang="sass" scoped>

</style>
