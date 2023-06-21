<script>
export default {
  name: "ButtonToDropdown",
  props: {
    /**
     * slot 数量超过多少,才被转换为《更多下拉列表》
     */
    sliceNumber: {
      type: Number,
      default: 3
    },
    moreText: {
      type: String,
      default: "更多"
    }
  },

  render(h) {
    const defaultSlotEl = this.$slots.default;
    let buttons = [];
    let dropdownItems = [];
    if (defaultSlotEl?.length) {
      // 存在的按钮
      const existButtons = defaultSlotEl.filter(item => {
        if (item.tag) {
          return item;
        }
      });
      const sliceNumber = this.sliceNumber || 0;
      if (existButtons.length <= sliceNumber) {
        buttons = existButtons.slice(0, sliceNumber);
      } else {
        buttons = existButtons.slice(0, sliceNumber - 1);
        dropdownItems = existButtons.slice(sliceNumber - 1);
      }
      let dropdown = [];
      if (dropdownItems.length) {
        const dropdownItem = dropdownItems.map(e => {
          return h("el-dropdown-item", {}, [e]);
        });
        dropdown = h(
          "el-dropdown",
          {
            style: {
              "margin-left": "24px"
            },
            props: {
                ...this.$attrs
            }
          },
          [
            h("el-button", {
              props: {
                type: "text"
              },
              domProps: {
                innerHTML: `${this.moreText} <i   class="el-icon-arrow-down "></i>`
              }
            }),
            h(
              "el-dropdown-menu",
              {
                slot: "dropdown"
              },
              dropdownItem
            )
          ]
        );
      }
      return h("div", [buttons, dropdown]);
    }
    return h(defaultSlotEl);
  }
};
</script>
