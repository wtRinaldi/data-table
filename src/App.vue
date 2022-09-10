<template>
  <div id="app">
    <table-basic
      :data="tableData"
      :columnOrder="renderOrder"
      ref="dataTable"
    >
      <table-element type="th">Currency</table-element>
      <table-element type="th">Amount</table-element>
      <template v-slot:body="data, csv">
        <table-element>{{ csv(data.currency) }}</table-element>
        <table-element>{{ csv(data.amount, 'end') }}</table-element>
      </template>
    </table-basic>
    <button @click="getData">Get CSV</button>
    <div>
      <div draggable="true">1</div>
      <div draggable="true">2</div>
      <div draggable="true">3</div>
      <div draggable="true">4</div>
      <div draggable="true">5</div>
    </div>
  </div>
</template>

<script>
import TableBasic from "./components/TableBasic.vue";
import TableElement from "./components/TableElement.vue";

export default {
  name: "App",
  components: {
    TableBasic,
    TableElement,
  },
  data() {
    return {
      renderOrder: [1, 0],
      tableData: [
        {
          amount: 10,
          currency: "USD",
        },
        {
          amount: 20,
          currency: "RUB",
        },
        {
          amount: 30,
          currency: "YEN",
        },
        {
          amount: 40,
          currency: "DEM",
        },
      ],
    };
  },
  methods: {
    getData() {
      console.log(this.$refs.dataTable.getCsv());
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
