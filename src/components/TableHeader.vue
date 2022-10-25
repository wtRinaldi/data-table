<script>
import Icon from "./Icon.vue";
export default {
  props: {
    drag: {
      type: Boolean,
    },
  },
  inject: ["dragStart"],
  render(createElement) {
    return createElement("th", {}, [
      createElement(
        "div",
        {
          style: {
            display: "flex",
            justifyContent: "space-between",
          },
        },
        [
          createElement("div", {}, this.$slots.default),
          this.drag
            ? createElement(
                "button",
                {
                  style: {
                    padding: "1rem",
                    cursor: "grab",
                    backgroundColor: "lightgrey",
                  },
                  on: {
                    mousedown: (e) => {
                      this.dragStart(e);
                    },
                  },
                },
                [
                  createElement(Icon, {
                    props: {
                      icon: "fa-solid fa-grip-lines-vertical",
                    },
                  }),
                ]
              )
            : "",
        ]
      ),
    ]);
  },
};
</script>
