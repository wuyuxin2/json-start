<template>
  <div>
    <div id="app">
      <h1>Bitcoin Price Index</h1>
      <div
        v-for="currency in info"
        class="currency"
        :key="currency.index"
      >
        {{ currency.description }}:
        <span class="lighten">
          <span v-html="currency.symbol"></span>{{ currency.rate_float | currencydecimal }}
        </span>
      </div>
    </div>
    <div>{{ info }}</div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      info: null
    };
  },
  filters: {
    currencydecimal(value) {
      return value.toFixed(2);
    }
  },
  mounted() {
    const axios = require("axios").default;
    axios
      .get("https://api.coindesk.com/v1/bpi/currentprice.json")
      .then(response => (this.info = response.data.bpi))
      .catch(error => console.log(error));
  },
  components: {}
};
</script>

<style>
body {
  background-color: #7f8d85;
  display: flex;
  justify-content: center;
}
#app {
  margin-top: 100px;
  background-color: #2f242c;
  width: 60%;
  border-radius: 1em;
  height: 200px;
}
h1,
.currency {
  text-align: center;
  color: #afb9b3;
}
.lighten {
  color: aliceblue;
}
</style>
