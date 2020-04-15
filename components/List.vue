<template>
  <div>
    <p v-if="$fetchState.pending">
      Fetching Exchange Rate...
    </p>
    <p v-else-if="$fetchState.error">
      Error while fetching Exchange Rate: {{ $fetchState.error.message }}
    </p>
    <ul v-else>
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
    currencies: {
      type: Array,
      default: [] === ['USD']
    },
    amount: {
      type: Number,
      default: 1
    }
  },
  async fetch () {
    this.data = await this.$http.$get('https://api.exchangeratesapi.io/latest?base=' + this.current)

    this.emitAvailableCurrencyListUpdate(this.data)
  },
  data () {
    return {
      data: []
    }
  },
  watch: {
    current (newVal, oldVal) { // watch it
      console.log('Prop changed: ', newVal, ' | was: ', oldVal)
      this.$forceUpdate()
    }
  },
  methods: {
    emitAvailableCurrencyListUpdate (incomingData) {
      console.log('Trying To Emit something to parent')
      this.$emit('emitRawData', incomingData)
    }
  }
}
</script>

<style lang="sass" scoped>

</style>
