<script>
export default {
  props: {
    type: {
      type: String,
      default: "td",
    },
    order: {
      type: Array,
    },
  },
  computed: {
    hasNewOrder() {
      debugger;
      return this.order && this.order.length > 0;
    },
  },
  render(createElement) {
    return createElement(
      this.type,
      {},
      this.hasNewOrder
        ? this.order.map((num) => this.$slots.default[num])
        : this.$slots.default
    );
  },
};
</script>