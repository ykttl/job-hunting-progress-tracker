<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Header v-model="cellsNum"/>
    {{cellsNum}}
    <Cells v-bind:updatedCellsNum="updatedCellsNum"/>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Cells from "./components/Cells.vue";

export default {
  name: "app",
  components: {
    Header,
    Cells
  },
  data() {
    return {
      cellsNum: 0
    };
  },
  computed: {
    updatedCellsNum() {
      return this.cellsNum;
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
