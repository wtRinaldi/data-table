<script>
import TableElement from "./TableElement.vue";
import Test from "./Test.vue";

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
      drag: {
        overlay: null,
        element: null,
        index: null,
        x: null,
        placeholder: null,
      },
    };
  },
  provide() {
    return {
      dragStart: this.dragStart,
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
    createDraggableOverlay() {
      // const table = this.$el,
      //   tableLocation = table.getBoundingClientRect(),
      //   headers = document.querySelectorAll("thead tr th"),
      //   rows = document.querySelectorAll("tbody tr"),
      //   dragTableContainer = document.createElement("div");
      // dragTableContainer.style.display = "flex";
      // this.drag.overlay = dragTableContainer;
      // dragTableContainer.style.position = "absolute";
      // dragTableContainer.style.left = `${tableLocation.left}px`;
      // dragTableContainer.style.top = `${tableLocation.top}px`;
      // table.parentNode.insertBefore(dragTableContainer, table);
      // table.style.visibility = "hidden";
      // headers.forEach((head, index) => {
      //   const newTable = document.createElement("table"),
      //     tableHead = head.cloneNode(true),
      //     newRow = document.createElement("tr"),
      //     width = parseInt(window.getComputedStyle(head).width);
      //   newTable.id = `${index}`;
      //   newRow.appendChild(tableHead);
      //   newTable.appendChild(newRow);
      //   newTable.setAttribute("class", "clone-table");
      //   newTable.style.width = `${width}px`;
      //   rows.forEach((row) => {
      //     const cell = row.children[index].cloneNode(true),
      //       newRow = document.createElement("tr");
      //     newRow.appendChild(cell);
      //     newTable.appendChild(newRow);
      //   });
      //   dragTableContainer.appendChild(newTable);
      // });
    },
    dragStart(e) {
      // this.createDraggableOverlay();
      // this.drag.x = e.clientX;
      // document.addEventListener("mousemove", this.dragElement);
      // document.addEventListener("mouseup", this.dragEnd);
    },
    dragElement(e) {
      // this.drag.index = e.currentTarget.closest("table").id;
      // this.drag.element = document.querySelector("table");
      // this.drag.element.classList.add("dragging");
      // this.drag.placeholder = document.createElement("div");
      // this.drag.placeholder.classList.add("placeholder");
      // this.drag.element.parentNode.insertBefore(
      //   this.drag.placeholder,
      //   this.drag.element.nextSibling
      // );
      // this.drag.placeholder.style.width = `${this.drag.element.offsetWidth}px`;
      // this.drag.element.style.position = "absolute";
      // this.drag.element.style.left = `${
      //   e.clientX - this.drag.element.clientWidth
      // }px`;
      // const prevEle = this.drag.element.previousElementSibling;
      // const nextEle = this.drag.placeholder.nextElementSibling;
      // if (prevEle && this.isOnLeft(this.drag.element, prevEle)) {
      //   this.swap(this.drag.placeholder, this.drag.element);
      //   this.swap(this.drag.placeholder, prevEle);
      //   return;
      // }
      // if (nextEle && this.isOnLeft(nextEle, this.drag.element)) {
      //   this.swap(nextEle, this.drag.placeholder);
      //   this.swap(nextEle, this.drag.element);
      // }
    },
    dragEnd() {
      // console.log("dragEnd");
      // this.drag.overlay.remove();
      // this.$el.style.visibility = "visible";
      // document.removeEventListener("mousemove", this.dragElement);
      // document.removeEventListener("mouseup", this.dragEnd);
    },
  },
  created() {
    this.csv = "";
    this.renderValues = null;
  },
  render(createElement) {
    return createElement("div", {}, [
      createElement("table", {}, [
        createElement("thead", {}, [
          createElement(
            TableElement,
            {
              props: {
                type: "tr",
                order: this.columnOrder,
              },
            },
            this.$slots.default.map((header, index) => {
              header.key = index;
              return header;
            })
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
              this.$scopedSlots.body(row)
            )
          )
        ),
      ]),
      createElement(
        "div",
        {
          style: {
            display: "flex",
            justifyContent: "space-between",
          },
        },
        [
          this.$slots.default.map((header, index) => {
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
                  [header]
                ),
              ]),
              createElement("tbody", {}, [
                this.data.map((row) => {
                  return createElement("tr", {}, this.$scopedSlots.body(row));
                }),
              ]),
            ]);
          }),
        ]
      ),
    ]);
  },
};
</script>
<style>
table {
  border-collapse: collapse;
  width: 100%;
}

table thead {
  background-color: #04aa6d;
  color: white;
}

table td {
  padding: 1rem;
}

table th {
  padding: 1rem;
  border: 1px solid black;
}

td {
  border: 1px solid black;
}

table tr:nth-child(even) {
  background-color: #f2f2f2;
}

table tbody tr:hover {
  background-color: #ddd;
}

.clone-list {
  display: flex;
}

.placeholder {
  background-color: #edf2f7;
  border: 2px dashed #cbd5e0;
}

.dragging {
  z-index: 999;
}
</style>
