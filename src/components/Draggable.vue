<script>
export default {
  props: {
    order: {
      type: Array,
    },
  },
  render(createElement) {
    return createElement(
      "tr",
      {},
      this.order.map((num) => this.$slots.default[num])
    );
  },
};
</script>