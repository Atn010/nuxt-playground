<template>
  <div class="global-sizing">
    <NavigationBar />
    <h1>Currency Convertion</h1>
    <p>Convert Currency</p>
    <h1>A Dollar Today is...</h1>
    <p v-if="$fetchState.pending">
      Fetching Exchange Rate...
    </p>
    <p v-else-if="$fetchState.error">
      Error while fetching Exchange Rate: {{ $fetchState.error.message }}
    </p>
    <ul v-else>
      <List
        :current="selectedCurrency"
        :currencies="Currency"
        :data="data"
        :amount="userInput"
      />
      <br><br><br>
      <li v-for="(value, key) of data.rates" :key="key">
        {{ key }} : {{ value }}
      </li>
    </ul>
  </div>
</template>

<script>
import NavigationBar from '~/components/Navigation.vue'
import List from '~/components/List.vue'
export default {
  components: {
    NavigationBar,
    List
  },
  async fetch () {
    this.data = await this.$http.$get('https://api.exchangeratesapi.io/latest?base=USD')
  },
  data () {
    return {
      data: [],
      Currency: ['SGD', 'IDR', 'EUR', 'MYR', 'USD'],
      userInput: 10000,
      selectedCurrency: 'USD'
    }
  }
}
</script>
<style>
</style>
