<template>
  <div id="app">
    <div class="px-16">
      <table-basic
        :data="tableData"
        :columnOrder="renderOrder"
        ref="dataTable"
      >
        <table-header drag>Currency</table-header>
        <table-header drag>Amount</table-header>
        <table-header drag>Color</table-header>
        <template v-slot:body="data">
          <table-element>{{ data.currency }}</table-element>
          <table-element>{{ data.amount }}</table-element>
          <table-element>{{ data.color }}</table-element>
        </template>
      </table-basic>
    </div>
    <button @click="getData">Get CSV</button>
  </div>
</template>

<script>
import TableBasic from "./components/TableBasic.vue";
import TableElement from "./components/TableElement.vue";
import TableHeader from "./components/TableHeader.vue";

export default {
  name: "App",
  components: {
    TableBasic,
    TableElement,
    TableHeader,
  },
  data() {
    return {
      renderOrder: [0, 1, 2],
      tableData: [
        {
          amount: 10,
          currency: "USD",
          color: "green",
        },
        {
          amount: 20,
          currency: "RUB",
          color: "blue",
        },
        {
          amount: 30,
          currency: "YEN",
          color: "purple",
        },
        {
          amount: 40,
          currency: "DEM",
          color: "red",
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
