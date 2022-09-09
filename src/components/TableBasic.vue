<script>
import TableElement from "./TableElement.vue";
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
  },
  render(createElement) {
    return createElement("table", {}, [
      createElement("thead", {}, [
        createElement(
          TableElement,
          {
            props: {
              type: "tr",
              order: this.columnOrder,
            },
          },
          this.$slots.default
        ),
      ]),
      createElement(
        "tbody",
        {},
        this.data.map((row) =>
          createElement(
            TableElement,
            {
              props: {
                type: "tr",
                order: this.columnOrder,
              },
            },
            this.$scopedSlots.body(row, this.addCsv)
          )
        )
      ),
      createElement("tr", {}, this.order),
    ]);
  },
};
</script>
