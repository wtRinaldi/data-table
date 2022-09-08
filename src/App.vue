<template>
  <div id="app">
    <table-basic
      :data="tableData"
      ref="dataTable"
    >
      <draggable :order="renderOrder">
        <table-element type="th">Currency</table-element>
        <table-element type="th">Amount</table-element>
      </draggable>
      <template v-slot:body="data, csv">
        <draggable :order="renderOrder">
          <table-element>{{ csv(data.currency) }}</table-element>
          <table-element>{{ csv(data.amount, 'end') }}</table-element>
        </draggable>
      </template>
    </table-basic>
    <button @click="getData">Get CSV</button>
  </div>
</template>

<script>
import TableBasic from "./components/TableBasic.vue";
import TableElement from "./components/TableElement.vue";
import Draggable from "./components/Draggable.vue";

export default {
  name: "App",
  components: {
    TableBasic,
    TableElement,
    Draggable,
  },
  data() {
    return {
      renderOrder: [0, 1],
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
    clearCsv() {
      debugger;
      this.$refs.dataTable.clearCsv();
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
