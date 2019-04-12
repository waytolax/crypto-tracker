<template>
  <div id="app">
    <CurrenciesTable />
  </div>
</template>

<script>
import CurrenciesTable from "./components/CurrenciesTable";

export default {
  components: {
    CurrenciesTable
  }
};
</script>

<style>
body {
  margin: 0;
}
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 50px 5px;
  box-sizing: border-box;
  background: linear-gradient(90deg, #fd8355 0%, #f0576c 37%, #f79cbd 100%);
}
</style>
