<template>
  <div id="app">
    {{ info }}
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      info: null
    }
  },
  mounted() {
    const axios = require('axios').default;
    axios
      .get('https://api.coindesk.com/v1/bpi/currentprice.json')
      .then(response => (this.info = response))
  },
  components: {}
};
</script>

<style>
</style>
