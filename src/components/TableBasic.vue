<script>
export default {
  props: {
    data: {
      type: Array,
      required: true,
    },
    columnOrder: {
      type: Array,
    },
  },
  data() {
    return {
      order: null,
    };
  },
  methods: {
    addCsv(value, modifier) {
      modifier === undefined ? (modifier = ", ") : (modifier = "\n");
      this.csv += value + modifier;

      return value;
    },
    getCsv() {
      return this.csv;
    },
  },
  created() {
    this.csv = "";
    this.order = this.columnOrder
      ? this.columnOrder
      : [...Array(this.data.length)];
  },
  render(createElement) {
    return createElement("table", {}, [
      // createElement("thead", {}, [
      //   createElement("tr", {}, this.$slots.default),
      // ]), removed for draggable
      createElement("thead", {}, this.$slots.default),
      createElement(
        "tbody",
        {},
        this.data.map((row) =>
          createElement("tr", {}, this.$scopedSlots.body(row, this.addCsv))
        )
      ),
      createElement("tr", {}, this.csv),
    ]);
  },
};
</script>
