<script>
export default {
  props: {
    type: {
      type: String,
      default: "td",
    },
  },
  render(createElement) {
    return createElement(this.type, {}, this.$slots.default);
  },
};
</script>