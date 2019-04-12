<template>
  <div class="wrapper">
    <table>
      <tr>
        <th>Currency</th>
        <th>Price</th>
      </tr>
      <tr v-for="c of sortedByPrice" :key="c.CoinInfo.Id">
        <td>{{ c.CoinInfo.FullName }}</td>
        <td>{{ c.DISPLAY.USD.PRICE }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      currencies: []
    };
  },
  computed: {
    sortedByPrice() {
      return this.currencies.sort((a, b) => b.RAW.USD.PRICE - a.RAW.USD.PRICE);
    }
  },
  mounted() {
    this.getCurrencies();
    const intervalId = setInterval(() => this.getCurrencies(), 30000);
  },
  methods: {
    getCurrencies() {
      axios
        .get(
          "https://min-api.cryptocompare.com/data/top/mktcapfull?limit=50&tsym=USD"
        )
        .then(res => {
          if (res.data.Response === "Error") console.log(res.data.Message);
          else this.currencies = res.data.Data;
        });
    }
  }
};
</script>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  width: 100%;
  max-width: 600px;
  height: 80vh;
  padding: 20px;
  box-sizing: border-box;
  overflow: auto;
  background: linear-gradient(
    to left,
    rgb(255, 255, 255) 0%,
    rgb(238, 238, 238) 49%,
    rgb(237, 237, 237) 100%
  );
  border-radius: 5px;
  box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.5);
}

table {
  text-align: center;
  border-collapse: collapse;
}
tr {
  width: 50%;
  border-bottom: 1px solid #c0c0c0;
}
th,
td {
  padding: 5px 0;
}
</style>
