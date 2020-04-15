<template>
  <div class="global-sizing">
    <NavigationBar />
    <h1>Currency Convertion</h1>
    <p>Convert Currency</p>
    <div>
      <div class="dropdown">
        <button class="dropbtn">
          Dropdown
        </button>
        <div class="dropdown-content">
          <div v-for="(value, index) of currencyDataList" :key="index">
            <button @click="updateSelectedCurrency(value)">
              {{ value }}
            </button>
          </div>
        </div>
      </div>
      <div>
        <input v-model="userInput" placeholder="10000" name="userInput" type="number">
      </div>
    </div>
    <list
      :current="selectedCurrency"
      :currencies="Currency"
      :amount="userInput"
      @emitRawData="updateCurrencyDataList"
    />
  </div>
</template>

<script>
import axios from 'axios'
import NavigationBar from '~/components/Navigation.vue'
import List from '~/components/List.vue'
export default {
  components: {
    NavigationBar,
    List
  },
  asyncData () {
    return axios
      .get('https://api.exchangeratesapi.io/latest?base=' + 'USD')
      .then((result) => {
        return {
          exchange: Object.keys(result.data.rates)
        }
      })
  },
  data () {
    return {
      data: [],
      currencyDataList: ['USD', 'SGD', 'EUR'],
      Currency: ['SGD', 'IDR', 'EUR', 'MYR', 'USD'],
      userInput: 10000,
      selectedCurrency: 'USD'
    }
  },
  methods: {
    updateCurrencyDataList (incomingData) {
      console.log('Trying To Emit something to parent2')
      for (const key in incomingData.rates) {
        if (!this.currencyDataList.includes(key)) {
          this.currencyDataList.push(key)
        }
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
  padding: 16px;
  text-align: center;
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
