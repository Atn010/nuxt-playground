<template>
  <div>
    <p v-if="$fetchState.pending">
      Fetching Exchange Rate...
    </p>
    <p v-else-if="$fetchState.error">
      Error while fetching Exchange Rate: {{ $fetchState.error.message }}
    </p>
    <ul v-else>
      <ul v-for="(item, index) in displayCurrencyList" :key="index">
        <li>
          <br>
          <Row
            :current="current"
            :currency="item"
            :rate="data.rates[item]"
            :amount="amount"
          />
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
      data: [],
      displayCurrencyList: ['SGD', 'IDR', 'EUR', 'MYR', 'USD'],
      choiceList: []
    }
  },
  watch: {
    current (newVal, oldVal) {
      this.fetchAgain()
    },
    displayCurrencyList () {
      console.log('Making new list1')
      this.generateNewChoice()
    },
    currencies () {
      console.log('Making new list2')
      this.generateNewChoice()
    }
  },
  methods: {
    emitAvailableCurrencyListUpdate (incomingData) {
      this.$emit('emitRawData', incomingData)
    },
    async fetchAgain () {
      this.data = await this.$http.$get('https://api.exchangeratesapi.io/latest?base=' + this.current)
    },
    generateNewChoice () {
      console.log('Making new list3')
      this.choiceList = this.currencies.filters(this.displayCurrencyList)
    }
  }
}
</script>

<style lang="sass" scoped>

</style>
