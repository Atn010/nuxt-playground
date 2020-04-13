<template>
  <div class="global-sizing">
    <NavigationBar />
    <h1>Currency Convertion</h1>
    <p>Convert Currency</p>
    <p v-if="$fetchState.pending">
      Fetching Exchange Rate...
    </p>
    <p v-else-if="$fetchState.error">
      Error while fetching Exchange Rate: {{ $fetchState.error.message }}
    </p>
    <ul v-else>
      <div>
        <div class="dropdown">
          <button class="dropbtn">
            Dropdown
          </button>
          <div class="dropdown-content">
            <button v-for="(value, index) of currencyDataList" :key="index" @click="updateSelectedCurrency(value)">
              {{ value }}
            </button>
          </div>
        </div>
        <div>
          <input v-model="userInput" placeholder="10000" name="userInput" type="number">
        </div>
      </div>
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
    this.data = await this.$http.$get('https://api.exchangeratesapi.io/latest?base=' + this.selectedCurrency)

    this.updateCurrencyDataList(this.data)
  },
  data () {
    return {
      data: [],
      currencyDataList: ['USD'],
      Currency: ['SGD', 'IDR', 'EUR', 'MYR', 'USD'],
      userInput: 10000,
      selectedCurrency: 'USD'
    }
  },
  methods: {
    updateCurrencyDataList (incomingData) {
      for (const key in incomingData.rates) {
        this.currencyDataList.push({ key })
      }
    },
    updateSelectedCurrency (data) {
      this.selectedCurrency = data
    }
  }
}
</script>
<style>
.dropbtn {
  background-color: #4CAF50;
  color: white;
  padding: 16px;
  font-size: 16px;
  border: none;
  cursor: pointer;
}

/* The container <div> - needed to position the dropdown content */
.dropdown {
  position: relative;
  display: inline-block;
}

/* Dropdown Content (Hidden by Default) */
.dropdown-content {
  display: none;
  position: absolute;
  background-color: #f9f9f9;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
  z-index: 1;
}

/* Links inside the dropdown */
.dropdown-content a {
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
}

/* Change color of dropdown links on hover */
.dropdown-content a:hover {background-color: #f1f1f1}

/* Show the dropdown menu on hover */
.dropdown:hover .dropdown-content {
  display: block;
}

/* Change the background color of the dropdown button when the dropdown content is shown */
.dropdown:hover .dropbtn {
  background-color: #3e8e41;
}
</style>
